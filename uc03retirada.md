# Especificação de Requisitos Funcionais
# Caso de Uso (CDU) — UC03: Registrar Retirada de Equipamento
 
## Histórico de Versões
 
| Data | Versão | Descrição | Autor |
|------|--------|-----------|-------|
| 14/05/2026 | 1.0 | Criação inicial do caso de uso | Equipe GAC |
 
---
 
## 1. Nome do Caso de Uso
 
Registrar Retirada de Equipamento
 
---
 
## 2. Objetivo
 
Registrar formalmente a saída de um equipamento do CCT para uso por um Professor, por meio da leitura de identificador físico (NFC ou QR Code), atualizando o status do item no inventário e vinculando a responsabilidade ao usuário.
 
---
 
## 3. Tipo de Caso de Uso
 
Concreto.
 
---
 
## 4. Atores
 
### 4.1 Primário
 
**Professor** — inicia e conduz a retirada do equipamento, realizando a leitura do identificador e assinando o termo de responsabilidade.
 
### 4.2 Secundário
 
**Atendente** — auxilia o Professor no processo de retirada presencial quando necessário.
 
---
 
## 5. Precondições
 
- O usuário deve estar autenticado no sistema (UC01 concluído).
- O equipamento deve estar com status "Disponível" no inventário (RN01).
- O Professor não pode possuir outro projetor emprestado simultaneamente (RN04).
- O equipamento deve possuir etiqueta NFC ou QR Code ativa e legível.
---
 
## 6. Fluxo Principal
 
**P1. Acesso à funcionalidade de retirada**
O Professor acessa a opção "Retirar Equipamento" no aplicativo mobile e o sistema exibe a tela de leitura de identificador.
 
**P2. Leitura do identificador físico**
O Professor aproxima o smartphone da etiqueta NFC ou aponta a câmera para o QR Code fixado no equipamento e o sistema captura o identificador único do item.
 
**P3. Validação do equipamento**
O sistema verifica o identificador lido, confirma que o equipamento existe no inventário e que seu status é "Disponível".
 
**P4. Exibição dos dados do equipamento**
O sistema exibe as informações do equipamento identificado: nome, código, categoria, lista de acessórios inclusos e prazo padrão de devolução (conforme RN08).
 
**P5. Inclusão do Termo de Responsabilidade**
O sistema aciona automaticamente o fluxo UC04 — Assinar Termo Digital para que o Professor formalize a responsabilidade pelo equipamento.
 
**P6. Confirmação da retirada**
Após a assinatura do termo (UC04 concluído), o sistema registra a retirada com: identificador do equipamento, matrícula do Professor, data/hora de saída e prazo de devolução.
 
**P7. Atualização do status**
O sistema atualiza o status do equipamento para "Emprestado" e exibe a confirmação: *"Retirada registrada com sucesso. Devolva até [data/hora limite]."*
 
---
 
## 7. Fluxos Alternativos
 
**A1. Retirada auxiliada pelo Atendente**
 
> Originado em P2, quando o Professor não possui smartphone compatível com NFC.
 
A1.1. O Atendente realiza a leitura do identificador NFC ou QR Code pelo terminal do balcão.
A1.2. O Atendente informa a matrícula do Professor no sistema.
A1.3. O fluxo segue a partir do passo P3, com o Professor realizando a assinatura digital na tela do terminal.
 
---
 
## 8. Fluxos de Exceção
 
**E1. Equipamento indisponível**
 
> Originado em P3, quando o status do equipamento não é "Disponível".
 
E1.1. O sistema exibe a mensagem: *"Este equipamento não está disponível para retirada. Status atual: [status do item]."*
E1.2. O sistema sugere consultar outros equipamentos disponíveis (UC02).
E1.3. O fluxo é encerrado.
 
**E2. Identificador não reconhecido**
 
> Originado em P3, quando o código lido não corresponde a nenhum item do inventário.
 
E2.1. O sistema exibe a mensagem: *"Equipamento não identificado. Verifique a etiqueta ou solicite auxílio ao Atendente."*
E2.2. O sistema retorna ao passo P2.
 
**E3. Professor com empréstimo ativo não autorizado**
 
> Originado em P3, quando o Professor já possui um projetor emprestado (RN04).
 
E3.1. O sistema exibe a mensagem: *"Você já possui um equipamento desta categoria em seu nome. Devolva-o antes de realizar nova retirada."*
E3.2. O fluxo é encerrado.
 
**E4. Falha na leitura do identificador**
 
> Originado em P2, quando NFC ou QR Code não é lido após 3 tentativas.
 
E4.1. O sistema exibe a mensagem: *"Não foi possível ler o identificador. Tente novamente ou informe o código manualmente."*
E4.2. O sistema exibe campo para inserção manual do código do equipamento.
E4.3. O fluxo retorna ao passo P3.
 
---
 
## 9. Pós-condições
 
- O equipamento tem seu status alterado para "Emprestado".
- A retirada é registrada no histórico do equipamento e do Professor.
- O Professor recebe confirmação com o prazo de devolução.
- O sistema agenda o envio de notificação de lembrete de devolução (UC09).
---
 
## 10. Requisitos Não Funcionais
 
- **RNF02** — A leitura do NFC/QR Code e o carregamento da tela de confirmação devem ser concluídos em até 2 segundos.
- **RNF09** — A funcionalidade deve operar em smartphones Android 10+ com suporte a NFC e câmera.
- O registro da retirada deve ser persistido imediatamente, sem necessidade de ação adicional do usuário.
---
 
## 11. Ponto de Extensão
 
**PE1. Assinar Termo Digital (UC04)**
No passo P5, o sistema aciona obrigatoriamente o UC04 — Assinar Termo Digital. A retirada só é concluída após a assinatura ser confirmada. Caso o Professor recuse o termo, a retirada é cancelada e o fluxo é encerrado.
 
---
 
## 12. Frequência de Utilização
 
**Alta** — ocorre múltiplas vezes ao dia, concentrada nos períodos de início de aula (manhã: 07h–08h, tarde: 13h–14h, noite: 19h–20h).
 
---
 
## 13. Interface Visual
 
**IV1. Tela de Leitura de Identificador (Mobile)**
Área central com animação de leitura NFC e botão alternativo "Escanear QR Code". Botão "Inserir código manualmente" no rodapé.
 
**IV2. Tela de Confirmação da Retirada**
Exibe foto do equipamento, nome, acessórios, prazo de devolução e botão "Confirmar Retirada". Requer passagem obrigatória pela tela de assinatura (UC04) antes da confirmação final.
 
---
 
## 14. Observações
 
- A etiqueta NFC/QR Code deve ser fixada fisicamente em cada equipamento antes da ativação no sistema.
- Avaliar futuramente a possibilidade de retirada por agendamento prévio.
---
 
## 15. Referências
 
- RNF02, RNF09 — Especificação de Requisitos Não Funcionais do sistema GAC.
- RN01, RN03, RN04, RN08 — Regras de Negócio aplicáveis à retirada.
- UC01 — Realizar Login (precondição).
- UC02 — Consultar Disponibilidade (pré-etapa recomendada).
- UC04 — Assinar Termo Digital (include obrigatório).
- UC09 — Enviar Notificações (pós-condição: agendamento de lembrete).
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
 