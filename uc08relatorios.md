# Especificação de Requisitos Funcionais
# Caso de Uso (CDU) — UC08: Gerar Relatórios de Utilização
 
## Histórico de Versões
 
| Data | Versão | Descrição | Autor |
|------|--------|-----------|-------|
| 14/05/2026 | 1.0 | Criação inicial do caso de uso | Equipe GAC |
 
---
 
## 1. Nome do Caso de Uso
 
Gerar Relatórios de Utilização
 
---
 
## 2. Objetivo
 
Permitir que o Administrador gere relatórios analíticos sobre o uso dos equipamentos do CCT, consolidando informações de retiradas, devoluções, atrasos e ocorrências para apoiar a tomada de decisão baseada em dados.
 
---
 
## 3. Tipo de Caso de Uso
 
Concreto.
 
---
 
## 4. Atores
 
### 4.1 Primário
 
**Administrador** — seleciona os parâmetros do relatório, aciona a geração e interpreta os resultados para fins de gestão.
 
### 4.2 Secundário
 
Não se aplica.
 
---
 
## 5. Precondições
 
- O usuário deve estar autenticado com perfil "Administrador" (UC01 concluído — RN14).
- Devem existir registros de movimentação no sistema para o período selecionado.
---
 
## 6. Fluxo Principal
 
**P1. Acesso à funcionalidade de relatórios**
O Administrador acessa a seção "Relatórios" no painel web e o sistema exibe a tela de configuração de relatórios com os tipos disponíveis.
 
**P2. Seleção do tipo de relatório**
O Administrador seleciona o tipo de relatório desejado entre as opções: "Utilização por Equipamento", "Utilização por Professor", "Ocorrências e Avarias", "Atrasos de Devolução" ou "Inventário Geral".
 
**P3. Configuração dos filtros e período**
O Administrador define os filtros aplicáveis ao tipo de relatório selecionado: período (data início e data fim), categoria de equipamento, nome do Professor ou equipamento específico.
 
**P4. Geração do relatório**
O Administrador aciona o botão "Gerar Relatório" e o sistema processa os dados conforme os parâmetros informados.
 
**P5. Exibição do relatório**
O sistema exibe o relatório na tela com: tabelas de dados, gráficos de utilização, indicadores resumidos (total de retiradas, taxa de ocupação, número de ocorrências) e observações relevantes.
 
**P6. Exportação do relatório**
O Administrador seleciona o formato de exportação desejado (PDF ou CSV) e aciona "Exportar". O sistema gera o arquivo e disponibiliza o download.
 
---
 
## 7. Fluxos Alternativos
 
**A1. Relatório sem dados no período selecionado**
 
> Originado em P5, quando não há registros para os filtros configurados.
 
A1.1. O sistema exibe a mensagem: *"Nenhum dado encontrado para o período e filtros selecionados. Ajuste os parâmetros e tente novamente."*
A1.2. O fluxo retorna ao passo P3.
 
**A2. Exportação somente em CSV**
 
> Originado em P6, quando o Administrador precisa dos dados brutos para tratamento externo.
 
A2.1. O Administrador seleciona "CSV" como formato.
A2.2. O sistema gera o arquivo com todos os registros em formato tabular e disponibiliza o download.
A2.3. O fluxo é encerrado.
 
---
 
## 8. Fluxos de Exceção
 
**E1. Falha no processamento do relatório**
 
> Originado em P4, quando o sistema não consegue processar os dados no tempo esperado.
 
E1.1. O sistema exibe a mensagem: *"Não foi possível gerar o relatório. Tente novamente ou reduza o período de análise."*
E1.2. O fluxo retorna ao passo P3.
 
**E2. Falha na exportação do arquivo**
 
> Originado em P6, quando a geração do arquivo falha.
 
E2.1. O sistema exibe a mensagem: *"Erro ao gerar o arquivo de exportação. Tente novamente."*
E2.2. O relatório permanece visível na tela para visualização manual.
 
---
 
## 9. Pós-condições
 
- O relatório foi gerado e exibido ao Administrador.
- Se exportado, o arquivo (PDF ou CSV) está disponível para download.
- Nenhuma alteração é realizada nos dados do inventário como resultado desta ação.
---
 
## 10. Requisitos Não Funcionais
 
- **RNF01** — Relatórios de períodos de até 3 meses devem ser gerados em até 3 segundos.
- Relatórios de períodos superiores a 3 meses podem ser processados de forma assíncrona, com notificação ao Administrador quando disponíveis.
- **RNF14** — Dados pessoais exibidos nos relatórios devem seguir as diretrizes da LGPD.
- **RNF15** — Os dados fonte dos relatórios devem ser mantidos por no mínimo 12 meses.
---
 
## 11. Ponto de Extensão
 
Não se aplica.
 
---
 
## 12. Frequência de Utilização
 
**Média** — estimada em uso semanal ou mensal pela equipe de gestão do CCT, com picos em períodos de avaliação institucional e planejamento de compras.
 
---
 
## 13. Interface Visual
 
**IV1. Tela de Configuração de Relatório**
Dropdown de tipo de relatório. Seletor de período (data início / data fim). Filtros adicionais (categoria, Professor, equipamento). Botão "Gerar Relatório".
 
**IV2. Tela de Exibição do Relatório**
Indicadores resumidos em cards no topo (total de retiradas, taxa de ocupação, nº de ocorrências). Gráfico de barras ou linha por período. Tabela detalhada com todos os registros. Botões "Exportar PDF" e "Exportar CSV" no topo direito.
 
---
 
## 14. Observações
 
- Avaliar futuramente a criação de relatórios agendados, enviados automaticamente por e-mail para o Administrador em periodicidade configurável.
- Os relatórios de "Ocorrências e Avarias" são especialmente relevantes para embasar decisões de manutenção e descarte (UC10, RN13).
---
 
## 15. Referências
 
- RNF01, RNF14, RNF15 — Especificação de Requisitos Não Funcionais do sistema GAC.
- RN14, RN16 — Regras de Negócio: controle de acesso e conteúdo dos relatórios.
- UC01 — Realizar Login (precondição — perfil Administrador).
- UC10 — Agendar Manutenção (relatórios de ocorrências subsidiam decisões de manutenção).
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