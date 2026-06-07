# Especificação de Requisitos Funcionais
# Caso de Uso (CDU) — UC05: Registrar Devolução de Equipamento
 
## Histórico de Versões
 
| Data | Versão | Descrição | Autor |
|------|--------|-----------|-------|
| 14/05/2026 | 1.0 | Criação inicial do caso de uso | Equipe GAC |
 
---
 
## 1. Nome do Caso de Uso
 
Registrar Devolução de Equipamento
 
---
 
## 2. Objetivo
 
Registrar formalmente o retorno de um equipamento ao CCT, realizando a conferência técnica do item por meio de checklist e atualizando o status do equipamento no inventário.
 
---
 
## 3. Tipo de Caso de Uso
 
Concreto.
 
---
 
## 4. Atores
 
### 4.1 Primário
 
**Atendente** — recebe o equipamento devolvido, conduz o processo de registro e executa o checklist técnico.
 
### 4.2 Secundário
 
**Administrador** — pode realizar a devolução quando o Atendente não está disponível.
**Professor** — entrega o equipamento e aguarda a confirmação do registro.
 
---
 
## 5. Precondições
 
- O usuário deve estar autenticado no sistema com perfil Atendente ou Administrador (UC01 concluído).
- O equipamento deve estar com status "Emprestado" no inventário.
- Deve existir um registro de retirada ativo vinculado ao equipamento.
---
 
## 6. Fluxo Principal
 
**P1. Acesso à funcionalidade de devolução**
O Atendente acessa a opção "Registrar Devolução" no sistema e o sistema exibe a tela de identificação do equipamento.
 
**P2. Identificação do equipamento devolvido**
O Atendente realiza a leitura do identificador NFC ou QR Code do equipamento entregue pelo Professor e o sistema localiza o registro de retirada ativo correspondente.
 
**P3. Exibição do registro de retirada**
O sistema exibe os dados da retirada vinculada: nome do Professor responsável, data/hora de saída, prazo de devolução e lista de acessórios que deveriam acompanhar o item.
 
**P4. Execução do checklist técnico**
O sistema aciona automaticamente o fluxo UC06 — Realizar Checklist Técnico para que o Atendente confira o estado do equipamento devolvido.
 
**P5. Confirmação da devolução**
Após a conclusão do checklist (UC06 concluído sem pendências), o Atendente confirma a devolução e o sistema registra: data/hora de devolução, identificador do Atendente e resultado do checklist.
 
**P6. Atualização do status**
O sistema atualiza o status do equipamento para "Disponível" e exibe a confirmação: *"Devolução registrada com sucesso. Equipamento disponível para novo empréstimo."*
 
---
 
## 7. Fluxos Alternativos
 
**A1. Devolução com atraso**
 
> Originado em P3, quando a data/hora atual é posterior ao prazo de devolução (RN09).
 
A1.1. O sistema destaca o atraso em vermelho na tela, exibindo: *"Devolução em atraso de [X horas/minutos]."*
A1.2. O sistema registra o atraso no histórico do Professor.
A1.3. Se o atraso for superior a 24 horas (RN10), o sistema sinaliza o bloqueio automático do Professor para novos empréstimos até regularização.
A1.4. O fluxo segue normalmente a partir do passo P4.
 
**A2. Checklist com pendências resolvidas no ato**
 
> Originado em P4, quando o checklist detecta divergência leve corrigida imediatamente (ex.: acessório encontrado na bolsa).
 
A2.1. O Atendente registra a observação no campo de comentários do checklist.
A2.2. O checklist é concluído como "aprovado com ressalva".
A2.3. O fluxo segue a partir do passo P5.
 
---
 
## 8. Fluxos de Exceção
 
**E1. Equipamento não localizado no sistema**
 
> Originado em P2, quando o identificador lido não corresponde a nenhuma retirada ativa.
 
E1.1. O sistema exibe a mensagem: *"Nenhuma retirada ativa encontrada para este equipamento. Verifique o identificador ou consulte o administrador."*
E1.2. O fluxo é encerrado.
 
**E2. Checklist com avaria identificada**
 
> Originado em P4, quando UC06 identifica dano não registrado na saída.
 
E2.1. O sistema abre automaticamente um registro de ocorrência vinculado ao Professor responsável pela última retirada (RN06).
E2.2. O status do equipamento é atualizado para "Em manutenção" ao invés de "Disponível".
E2.3. O Administrador é notificado sobre a ocorrência (UC09).
E2.4. O fluxo é encerrado com a devolução registrada como "Devolvido com ocorrência".
 
---
 
## 9. Pós-condições
 
- O equipamento tem seu status atualizado (para "Disponível" ou "Em manutenção", conforme resultado do checklist).
- O registro de devolução é vinculado ao histórico do equipamento e do Professor.
- O Atendente responsável pela conferência é identificado no registro.
- Em caso de atraso, o histórico do Professor é atualizado conforme RN09 e RN10.
---
 
## 10. Requisitos Não Funcionais
 
- **RNF01** — O registro da devolução deve ser processado em até 3 segundos após a confirmação.
- **RNF03** — O status do equipamento deve ser atualizado em tempo real no inventário assim que a devolução for confirmada.
---
 
## 11. Ponto de Extensão
 
**PE1. Realizar Checklist Técnico (UC06)**
No passo P4, o sistema aciona obrigatoriamente o UC06 — Realizar Checklist Técnico. A devolução só é concluída com "Disponível" após a aprovação do checklist. Resultado com avaria redireciona para o fluxo de exceção E2.
 
---
 
## 12. Frequência de Utilização
 
**Alta** — ocorre a cada retirada registrada, com concentração nos horários de encerramento de aulas e fechamento do CCT.
 
---
 
## 13. Interface Visual
 
**IV1. Tela de Identificação do Equipamento (Devolução)**
Área de leitura NFC/QR Code com botão de entrada manual do código. Exibe imediatamente o nome do Professor e o prazo da retirada ao identificar o item.
 
**IV2. Tela de Confirmação da Devolução**
Resumo: dados da retirada, resultado do checklist, campo de observações e botão "Confirmar Devolução". Status pós-devolução exibido em destaque (verde = Disponível / amarelo = Em manutenção).
 
---
 
## 14. Observações
 
- Caso o Professor devolva o equipamento fora do horário de funcionamento do CCT, avaliar mecanismo de devolução assistida ou caixa de devolução com registro automático.
- O campo de observações da devolução é livre e deve ser utilizado para registrar qualquer informação relevante que não se encaixe nos itens do checklist.
---
 
## 15. Referências
 
- RNF01, RNF03 — Especificação de Requisitos Não Funcionais do sistema GAC.
- RN05, RN06, RN07, RN09, RN10 — Regras de Negócio aplicáveis à devolução.
- UC01 — Realizar Login (precondição).
- UC06 — Realizar Checklist Técnico (include obrigatório).
- UC09 — Enviar Notificações (acionado em caso de avaria ou atraso).
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