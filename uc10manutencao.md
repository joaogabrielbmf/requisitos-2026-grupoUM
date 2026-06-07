# Especificação de Requisitos Funcionais
# Caso de Uso (CDU) — UC10: Agendar Manutenção de Equipamento
 
## Histórico de Versões
 
| Data | Versão | Descrição | Autor |
|------|--------|-----------|-------|
| 14/05/2026 | 1.0 | Criação inicial do caso de uso | Equipe GAC |
 
---
 
## 1. Nome do Caso de Uso
 
Agendar Manutenção de Equipamento
 
---
 
## 2. Objetivo
 
Registrar e acompanhar manutenções preventivas e corretivas dos equipamentos do CCT, bloqueando o item para empréstimos durante o período de manutenção e garantindo o retorno controlado ao inventário após sua conclusão.
 
---
 
## 3. Tipo de Caso de Uso
 
Concreto.
 
---
 
## 4. Atores
 
### 4.1 Primário
 
**Administrador** — identifica a necessidade de manutenção, agenda o serviço no sistema e gerencia o retorno do equipamento ao inventário.
 
### 4.2 Secundário
 
**Sistema (Automático)** — altera o status do equipamento automaticamente na data agendada e envia notificação ao Administrador (UC09).
 
---
 
## 5. Precondições
 
- O usuário deve estar autenticado com perfil "Administrador" (UC01 concluído — RN14).
- O equipamento deve estar cadastrado no sistema (UC07 concluído).
- O equipamento deve estar com status "Disponível" ou ter sido devolvido com ocorrência de avaria (fluxo E2 do UC05) para agendamento de manutenção corretiva.
---
 
## 6. Fluxo Principal
 
**P1. Acesso à funcionalidade de manutenção**
O Administrador acessa a seção "Inventário", localiza o equipamento desejado e aciona a opção "Agendar Manutenção". O sistema exibe o formulário de agendamento.
 
**P2. Preenchimento dos dados da manutenção**
O Administrador preenche os campos: tipo de manutenção (Preventiva ou Corretiva), descrição do serviço a ser realizado, data de início e data prevista de conclusão, e responsável pelo serviço (técnico interno ou empresa terceirizada).
 
**P3. Confirmação do agendamento**
O Administrador aciona o botão "Agendar" e o sistema registra a manutenção com status "Agendada" e exibe a confirmação: *"Manutenção agendada com sucesso para [data de início]."*
 
**P4. Alteração automática de status na data de início**
Na data de início informada, o sistema altera automaticamente o status do equipamento para "Em manutenção" (RN12), bloqueando novas retiradas, e envia notificação ao Administrador (UC09).
 
**P5. Acompanhamento da manutenção**
O Administrador acompanha o andamento pelo painel de manutenções ativas, podendo registrar atualizações de progresso no campo de observações.
 
**P6. Encerramento da manutenção**
Ao término do serviço, o Administrador acessa o registro da manutenção e aciona "Concluir Manutenção". O sistema solicita a confirmação do resultado: "Concluída com sucesso" ou "Equipamento inutilizado (baixa patrimonial)".
 
**P7. Atualização do status do equipamento**
Se concluída com sucesso, o sistema atualiza o status do equipamento para "Disponível" e registra a data de conclusão real. Se inutilizado, o sistema inicia o fluxo de baixa patrimonial com aprovação do Administrador (RN13).
 
---
 
## 7. Fluxos Alternativos
 
**A1. Manutenção agendada para um equipamento atualmente emprestado**
 
> Originado em P3, quando a data de início da manutenção é futura e o equipamento está emprestado.
 
A1.1. O sistema exibe o aviso: *"Este equipamento possui retirada ativa. O status será alterado para 'Em manutenção' automaticamente na data de início, independentemente da devolução."*
A1.2. O Administrador confirma o agendamento.
A1.3. O sistema notifica o Professor com empréstimo ativo sobre a manutenção agendada e a necessidade de devolução antes da data de início.
A1.4. O fluxo segue a partir do passo P3.
 
**A2. Reagendamento de manutenção**
 
> Originado em P5, quando a data de conclusão precisa ser postergada.
 
A2.1. O Administrador acessa o registro da manutenção e aciona "Reagendar".
A2.2. O Administrador informa a nova data prevista de conclusão e a justificativa.
A2.3. O sistema atualiza o registro e mantém o status do equipamento como "Em manutenção".
A2.4. O sistema notifica o Administrador sobre o reagendamento (UC09).
 
---
 
## 8. Fluxos de Exceção
 
**E1. Campos obrigatórios não preenchidos**
 
> Originado em P3, quando o formulário é enviado incompleto.
 
E1.1. O sistema destaca os campos obrigatórios não preenchidos em vermelho.
E1.2. O sistema exibe a mensagem: *"Preencha todos os campos obrigatórios antes de agendar."*
E1.3. O fluxo retorna ao passo P2.
 
**E2. Data de início no passado**
 
> Originado em P3, quando a data de início informada é anterior à data atual.
 
E2.1. O sistema exibe a mensagem: *"A data de início não pode ser anterior à data atual. Informe uma data válida."*
E2.2. O fluxo retorna ao passo P2.
 
**E3. Falha na alteração automática de status**
 
> Originado em P4, quando o sistema não consegue alterar o status na data programada.
 
E3.1. O sistema registra a falha no log e envia notificação de alerta ao Administrador.
E3.2. O Administrador altera o status manualmente acessando o registro do equipamento.
 
---
 
## 9. Pós-condições
 
- A manutenção está registrada no histórico do equipamento com todos os dados e resultado.
- O equipamento está com status atualizado ("Em manutenção", "Disponível" ou em processo de baixa) conforme o resultado da manutenção.
- O histórico de manutenções é preservado permanentemente para rastreabilidade do patrimônio.
---
 
## 10. Requisitos Não Funcionais
 
- **RNF12** — A alteração automática de status na data de início deve ocorrer sem interrupção do serviço.
- **RNF15** — O histórico de manutenções deve ser mantido por no mínimo 12 meses.
- A funcionalidade deve ser acessível exclusivamente via interface web (painel administrativo).
---
 
## 11. Ponto de Extensão
 
**PE1. Enviar Notificações (UC09)**
No passo P4, ao alterar o status do equipamento para "Em manutenção", o sistema aciona UC09 para notificar o Administrador e, se aplicável, o Professor com empréstimo ativo. Também acionado no passo A2.4 em caso de reagendamento.
 
---
 
## 12. Frequência de Utilização
 
**Média** — estimada em uso mensal ou conforme demanda de manutenções preventivas e ocorrências de avarias identificadas nas devoluções (UC05).
 
---
 
## 13. Interface Visual
 
**IV1. Formulário de Agendamento de Manutenção (Web)**
Campos: tipo de manutenção (radio: Preventiva / Corretiva), descrição do serviço (texto livre), data de início (seletor), data prevista de conclusão (seletor), responsável pelo serviço (texto livre). Campo de observações. Botões "Cancelar" e "Agendar".
 
**IV2. Painel de Manutenções Ativas (Web)**
Lista de equipamentos em manutenção com: nome, código GAC, tipo de manutenção, data de início, data prevista de conclusão, dias em manutenção e status. Botões de ação: "Reagendar", "Registrar Atualização" e "Concluir Manutenção".
 
---
 
## 14. Observações
 
- O histórico de manutenções é um insumo importante para os relatórios de gestão patrimonial (UC08) e para decisões de descarte e substituição de equipamentos (RN13).
- Avaliar futuramente a integração com o sistema de ordens de serviço da Unifor para registro centralizado de manutenções.
---
 
## 15. Referências
 
- RNF12, RNF15 — Especificação de Requisitos Não Funcionais do sistema GAC.
- RN12, RN13, RN14 — Regras de Negócio: manutenção, baixa patrimonial e controle de acesso.
- UC01 — Realizar Login (precondição — perfil Administrador).
- UC05 — Registrar Devolução (pode originar manutenção corretiva via fluxo de exceção E2).
- UC08 — Gerar Relatórios (histórico de manutenções subsidia relatórios de ocorrências).
- UC09 — Enviar Notificações (ponto de extensão PE1).
---
 
## 16. Checklist de Validação do Artefato (CDU)
 
### 16.1 Estrutura mínima
- [x] Nome do caso de uso iniciado com verbo no infinitivo.
- [x] Objetivo claro, direto e com foco em um objetivo principal.
- [x] Tipo do caso de uso informado (concreto/abstrato).
- [x] Atores primário e secundários identificados corretamente.
- [x] Precondições registradas.
- [x] Fluxo principal completo e coerente com o objetivo.
- [x] Fluxos alternativos e de exceção definidos.
- [x] Pós-condições registradas.
- [x] Requisitos não funcionais específicos do CDU registrados.
- [x] Pontos de extensão identificados.
- [x] Frequência de utilização estimada.
### 16.2 Qualidade da especificação
- [x] Passos escritos com linguagem simples e objetiva.
- [x] Ações descritas com verbos no presente do indicativo (3ª pessoa).
- [x] Alternância entre ação do ator e ação do sistema está clara.
- [x] Não há ambiguidade.
- [x] Regras de negócio e mensagens estão referenciadas.
### 16.3 Consistência e rastreabilidade
- [x] Pontos de entrada e saída dos fluxos alternativos estão explícitos.
- [x] Fluxos de exceção estão vinculados aos passos corretos.
- [x] Referências internas entre passos estão corretas.
- [x] Referências para RNF estão atualizadas.
### 16.4 Revisão final
- [x] Não há contradições entre seções do artefato.
- [ ] Documento revisado por pares.
- [ ] Artefato pronto para uso em desenvolvimento e testes.