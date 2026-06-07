# Especificação de Requisitos Funcionais
# Caso de Uso (CDU) — UC09: Enviar Notificações Automáticas
 
## Histórico de Versões
 
| Data | Versão | Descrição | Autor |
|------|--------|-----------|-------|
| 14/05/2026 | 1.0 | Criação inicial do caso de uso | Equipe GAC |
 
---
 
## 1. Nome do Caso de Uso
 
Enviar Notificações Automáticas
 
---
 
## 2. Objetivo
 
Comunicar proativamente professores e administradores sobre eventos relevantes do ciclo de vida dos equipamentos — como proximidade do prazo de devolução, atrasos, avarias registradas e manutenções agendadas — por meio de notificações automáticas enviadas pelo sistema.
 
---
 
## 3. Tipo de Caso de Uso
 
Concreto.
 
---
 
## 4. Atores
 
### 4.1 Primário
 
**Sistema (Automático)** — dispara as notificações com base em regras e eventos previamente configurados, sem necessidade de interação humana para iniciar o processo.
 
### 4.2 Secundário
 
**Professor** — destinatário das notificações de prazo, atraso e confirmação de retirada/devolução.
**Administrador** — destinatário das notificações de atraso crítico, avaria registrada e manutenção programada.
 
---
 
## 5. Precondições
 
- Deve existir um evento gatilho configurado no sistema (prazo próximo, atraso, avaria ou manutenção).
- O destinatário deve possuir e-mail institucional cadastrado e/ou ter o aplicativo mobile instalado com notificações push habilitadas.
- O serviço de envio de notificações deve estar ativo e acessível.
---
 
## 6. Fluxo Principal
 
**P1. Identificação do evento gatilho**
O sistema monitora continuamente os registros de empréstimo e inventário e identifica um evento que requer notificação: prazo de devolução em 2 horas, atraso superior a 30 minutos, avaria registrada ou manutenção agendada para o dia seguinte.
 
**P2. Composição da mensagem**
O sistema compõe a mensagem de notificação automaticamente com base no tipo de evento, incluindo: identificação do equipamento, tipo de ocorrência, prazo ou data relevante e instrução de ação para o destinatário.
 
**P3. Identificação do(s) destinatário(s)**
O sistema identifica os destinatários da notificação com base no tipo de evento: Professor responsável pelo equipamento, Administrador do CCT ou ambos.
 
**P4. Envio da notificação**
O sistema envia a notificação pelos canais configurados: e-mail institucional e/ou push notification no aplicativo mobile.
 
**P5. Registro do envio**
O sistema registra no log: tipo de evento, destinatário(s), canal(is) utilizado(s), data/hora do envio e status do envio (entregue ou falha).
 
---
 
## 7. Fluxos Alternativos
 
**A1. Notificação de confirmação de retirada**
 
> Disparado automaticamente ao término do UC03.
 
A1.1. O sistema envia ao Professor uma confirmação de retirada contendo: nome do equipamento, data/hora de saída e prazo de devolução.
A1.2. O fluxo segue a partir do passo P5.
 
**A2. Notificação de lembrete de devolução**
 
> Disparado automaticamente 2 horas antes do prazo limite (RN09).
 
A2.1. O sistema envia ao Professor a mensagem: *"Lembrete: o equipamento [nome] deve ser devolvido até [hora/data limite]."*
A2.2. O fluxo segue a partir do passo P5.
 
**A3. Notificação de manutenção agendada**
 
> Disparado automaticamente 24 horas antes da manutenção programada (UC10).
 
A3.1. O sistema envia ao Administrador a mensagem: *"Manutenção agendada para amanhã: equipamento [nome — código GAC] às [hora]."*
A3.2. O fluxo segue a partir do passo P5.
 
---
 
## 8. Fluxos de Exceção
 
**E1. Falha no envio por e-mail**
 
> Originado em P4, quando o servidor de e-mail não responde ou rejeita a mensagem.
 
E1.1. O sistema tenta o reenvio por e-mail até 3 vezes com intervalo de 5 minutos entre tentativas.
E1.2. Se todas as tentativas falharem, o sistema registra a falha no log e, se o aplicativo mobile estiver disponível, tenta o envio via push notification como canal alternativo.
E1.3. Se ambos os canais falharem, o sistema registra o evento como "Notificação não entregue" para revisão pelo Administrador.
 
**E2. Destinatário sem canal de notificação configurado**
 
> Originado em P3, quando o usuário não possui e-mail cadastrado e não tem o app instalado.
 
E2.1. O sistema registra a notificação como "Não enviada — sem canal disponível".
E2.2. O Administrador é alertado sobre a ausência de canal de comunicação para o usuário em questão.
 
---
 
## 9. Pós-condições
 
- A notificação foi enviada ao(s) destinatário(s) pelos canais disponíveis.
- O envio está registrado no log do sistema com status e detalhes do evento.
- Em caso de falha, o registro permite rastreabilidade para auditoria e reenvio manual.
---
 
## 10. Requisitos Não Funcionais
 
- **RNF17** — Notificações de atraso não podem ser desativadas pelo usuário final.
- As notificações devem ser enviadas em até 1 minuto após a identificação do evento gatilho.
- **RNF14** — O conteúdo das notificações não deve expor dados pessoais além do necessário para a identificação do evento (LGPD).
- **RNF15** — Os logs de envio de notificações devem ser mantidos por no mínimo 12 meses.
---
 
## 11. Ponto de Extensão
 
Não se aplica.
 
---
 
## 12. Frequência de Utilização
 
**Alta** — o sistema dispara notificações continuamente durante o horário de funcionamento do CCT; a frequência é diretamente proporcional ao volume de empréstimos ativos.
 
---
 
## 13. Interface Visual
 
**IV1. Central de Notificações (App Mobile)**
Lista cronológica de notificações recebidas com ícone de tipo (lembrete, atraso, avaria, manutenção), texto resumido e data/hora. Notificações não lidas destacadas em azul.
 
**IV2. Painel de Logs de Notificações (Web — Admin)**
Tabela com: data/hora, tipo de evento, equipamento, destinatário, canal utilizado e status de entrega (Entregue / Falha / Não enviado). Filtros por data, tipo e status.
 
---
 
## 14. Observações
 
- Avaliar futuramente o envio de notificações via WhatsApp ou SMS para aumentar a taxa de entrega em casos onde o e-mail não é verificado com frequência.
- O modelo de mensagem de cada tipo de notificação deve ser configurável pelo Administrador via painel de configurações.
---
 
## 15. Referências
 
- RNF14, RNF15, RNF17 — Especificação de Requisitos Não Funcionais do sistema GAC.
- RN09, RN10, RN17 — Regras de Negócio: atrasos e notificações automáticas.
- UC03 — Registrar Retirada (dispara notificação de confirmação).
- UC05 — Registrar Devolução (dispara notificação em caso de avaria).
- UC10 — Agendar Manutenção (dispara notificação de manutenção programada).
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
- [x] Pontos de extensão identificados (não se aplica).
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