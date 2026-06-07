# Especificação de Requisitos Funcionais
# Caso de Uso (CDU) — UC02: Consultar Disponibilidade de Equipamento
 
## Histórico de Versões
 
| Data | Versão | Descrição | Autor |
|------|--------|-----------|-------|
| 14/05/2026 | 1.0 | Criação inicial do caso de uso | Equipe GAC |
 
---
 
## 1. Nome do Caso de Uso
 
Consultar Disponibilidade de Equipamento
 
---
 
## 2. Objetivo
 
Permitir que o Professor ou Atendente verifique, em tempo real, o status de disponibilidade de um equipamento do inventário do CCT antes de efetuar uma retirada.
 
---
 
## 3. Tipo de Caso de Uso
 
Concreto.
 
---
 
## 4. Atores
 
### 4.1 Primário
 
**Professor** — inicia a consulta para verificar se o equipamento desejado está disponível antes de se deslocar ao CCT.
 
### 4.2 Secundário
 
**Atendente** — também pode realizar a consulta para verificar a disponibilidade durante o atendimento presencial.
 
---
 
## 5. Precondições
 
- O usuário deve estar autenticado no sistema (UC01 concluído).
- O inventário deve estar cadastrado e atualizado no sistema.
---
 
## 6. Fluxo Principal
 
**P1. Acesso à funcionalidade de consulta**
O Professor acessa a seção "Equipamentos" no menu do sistema e o sistema exibe a tela de consulta com filtros disponíveis.
 
**P2. Definição dos filtros de busca**
O Professor seleciona ou preenche os filtros desejados: categoria de equipamento (ex.: projetor, chave), sala ou localização, e/ou data desejada para uso.
 
**P3. Execução da busca**
O Professor aciona o botão "Buscar" e o sistema consulta o inventário em tempo real com base nos filtros informados.
 
**P4. Exibição dos resultados**
O sistema exibe a lista de equipamentos correspondentes aos filtros, indicando para cada item: nome, código, categoria, status atual (Disponível, Emprestado, Em manutenção, Indisponível) e localização no CCT.
 
**P5. Visualização do detalhe do equipamento**
O Professor seleciona um equipamento da lista e o sistema exibe a ficha detalhada: descrição, acessórios inclusos, foto e histórico resumido de uso.
 
---
 
## 7. Fluxos Alternativos
 
**A1. Nenhum equipamento encontrado com os filtros informados**
 
> Originado em P4, quando a busca não retorna resultados.
 
A1.1. O sistema exibe a mensagem: *"Nenhum equipamento encontrado com os critérios informados. Tente ajustar os filtros."*
A1.2. O sistema mantém a tela de consulta com os filtros preenchidos para que o usuário possa ajustá-los.
A1.3. O fluxo retorna ao passo P2.
 
**A2. Consulta sem filtros**
 
> Originado em P2, quando o usuário não preenche nenhum filtro.
 
A2.1. O sistema exibe todos os equipamentos do inventário com seus respectivos status.
A2.2. O fluxo segue para P5.
 
---
 
## 8. Fluxos de Exceção
 
**E1. Falha na consulta ao inventário**
 
> Originado em P3, quando o sistema não consegue acessar os dados do inventário.
 
E1.1. O sistema exibe a mensagem: *"Não foi possível carregar os equipamentos no momento. Tente novamente em instantes."*
E1.2. O sistema retorna ao passo P2.
 
---
 
## 9. Pós-condições
 
- O usuário visualizou o status atualizado do(s) equipamento(s) consultado(s).
- Nenhuma alteração é realizada no inventário como resultado desta consulta.
---
 
## 10. Requisitos Não Funcionais
 
- **RNF01** — O resultado da consulta deve ser exibido em até 3 segundos.
- **RNF03** — O inventário consultado deve refletir o status em tempo real, sem cache desatualizado.
- A tela de consulta deve ser acessível via mobile e web (RNF09).
---
 
## 11. Ponto de Extensão
 
Não se aplica.
 
---
 
## 12. Frequência de Utilização
 
**Alta** — a consulta de disponibilidade é realizada antes de cada retirada, múltiplas vezes ao dia, especialmente em horários de início de aula.
 
---
 
## 13. Interface Visual
 
**IV1. Tela de Consulta de Equipamentos**
Filtros: categoria (dropdown), localização (texto livre), data (seletor). Botão "Buscar". Lista de resultados com ícone de status colorido (verde = disponível, vermelho = indisponível, amarelo = em manutenção).
 
**IV2. Tela de Detalhe do Equipamento**
Foto do equipamento, nome, código, acessórios, status atual e histórico resumido (últimas 3 movimentações).
 
---
 
## 14. Observações
 
- O status "Disponível" deve ser atualizado automaticamente ao término de cada devolução (UC05).
- Avaliar futuramente a opção de reserva antecipada de equipamento a partir desta tela.
---
 
## 15. Referências
 
- RNF01, RNF03, RNF09 — Especificação de Requisitos Não Funcionais do sistema GAC.
- RN01 — Regra de Negócio: equipamento só pode ser retirado se status for "Disponível".
- UC01 — Realizar Login (precondição).
- UC03 — Registrar Retirada (continuação natural após consulta positiva).
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