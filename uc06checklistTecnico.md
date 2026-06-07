# Especificação de Requisitos Funcionais
# Caso de Uso (CDU) — UC06: Realizar Checklist Técnico
 
## Histórico de Versões
 
| Data | Versão | Descrição | Autor |
|------|--------|-----------|-------|
| 14/05/2026 | 1.0 | Criação inicial do caso de uso | Equipe GAC |
 
---
 
## 1. Nome do Caso de Uso
 
Realizar Checklist Técnico
 
---
 
## 2. Objetivo
 
Verificar sistematicamente o estado físico e a integridade dos acessórios de um equipamento no momento de sua devolução ao CCT, garantindo o registro do estado do item e identificando eventuais avarias ou itens faltantes.
 
---
 
## 3. Tipo de Caso de Uso
 
Abstrato — é sempre invocado por UC05 (Registrar Devolução de Equipamento) por meio de relacionamento «include», nunca iniciado diretamente pelo ator.
 
---
 
## 4. Atores
 
### 4.1 Primário
 
**Atendente** — conduz a verificação física do equipamento e preenche o checklist no sistema.
 
### 4.2 Secundário
 
**Administrador** — pode realizar o checklist quando o Atendente não está disponível.
 
---
 
## 5. Precondições
 
- O caso de uso UC05 — Registrar Devolução deve estar em execução (passo P4).
- O equipamento deve ter sido identificado e o registro de retirada deve ter sido localizado.
- O Atendente deve ter o equipamento físico em mãos para inspeção.
---
 
## 6. Fluxo Principal
 
**P1. Exibição do checklist**
O sistema exibe o formulário de checklist técnico correspondente à categoria do equipamento, contendo: lista de acessórios esperados, itens de verificação do estado físico (ex.: corpo, cabos, lente, controle remoto) e campo de observações gerais.
 
**P2. Verificação dos acessórios**
O Atendente confere fisicamente cada acessório listado e marca no sistema: "Presente" ou "Ausente" para cada item.
 
**P3. Verificação do estado físico**
O Atendente avalia o estado físico do equipamento principal e classifica cada item de verificação como: "OK", "Danificado" ou "N/A".
 
**P4. Registro fotográfico**
O Atendente captura foto(s) do equipamento devolvido pelo aplicativo ou terminal e o sistema as vincula ao registro de devolução.
 
**P5. Preenchimento de observações**
O Atendente preenche o campo de observações livres com qualquer informação adicional relevante (opcional, mas recomendado em caso de divergências).
 
**P6. Conclusão do checklist**
O Atendente aciona o botão "Concluir Checklist" e o sistema avalia automaticamente o resultado: se todos os acessórios estão presentes e nenhum item físico está "Danificado", o resultado é "Aprovado"; caso contrário, o resultado é "Reprovado com ocorrência".
 
**P7. Retorno ao fluxo chamador**
O sistema registra o resultado do checklist com data, hora e identificador do Atendente, e retorna ao UC05 com o resultado obtido.
 
---
 
## 7. Fluxos Alternativos
 
**A1. Acessório ausente justificado**
 
> Originado em P2, quando um acessório está ausente mas há justificativa (ex.: acessório era optativo ou já estava registrado como ausente na saída).
 
A1.1. O Atendente seleciona "Ausente" e aciona a opção "Registrar justificativa".
A1.2. O Atendente preenche a justificativa no campo específico.
A1.3. O sistema marca o item como "Ausente — justificado" e não contabiliza como pendência crítica.
A1.4. O fluxo retorna ao passo P2 para os demais itens.
 
**A2. Checklist sem câmera disponível**
 
> Originado em P4, quando o dispositivo não possui câmera funcional.
 
A2.1. O sistema exibe a opção de pular o registro fotográfico.
A2.2. O Atendente aciona "Pular foto" e o sistema registra a ausência de imagem com aviso: *"Checklist concluído sem registro fotográfico."*
A2.3. O fluxo segue para o passo P5.
 
---
 
## 8. Fluxos de Exceção
 
**E1. Avaria identificada não registrada na saída**
 
> Originado em P3, quando o Atendente marca item como "Danificado" e o estado de saída do item estava "OK".
 
E1.1. O sistema destaca o item em vermelho e solicita confirmação: *"Este dano não estava registrado na saída. Confirmar avaria?"*
E1.2. O Atendente confirma.
E1.3. O sistema registra a avaria e sinaliza ao UC05 que o checklist resultou em "Reprovado com ocorrência", redirecionando para o fluxo de exceção E2 do UC05.
 
**E2. Perda de conexão durante preenchimento**
 
> Originado em qualquer passo, quando a conexão com o servidor é perdida.
 
E2.1. O sistema salva localmente o progresso do checklist preenchido até o momento.
E2.2. O sistema exibe o aviso: *"Conexão perdida. Seu progresso foi salvo. O envio será realizado quando a conexão for restabelecida."*
E2.3. Ao restabelecer a conexão, o sistema sincroniza os dados salvos automaticamente.
 
---
 
## 9. Pós-condições
 
- O checklist está registrado no sistema com resultado ("Aprovado" ou "Reprovado com ocorrência"), data, hora e identificador do Atendente.
- As fotos do equipamento estão vinculadas ao registro de devolução.
- O resultado é retornado ao UC05 para determinar o status final do equipamento.
---
 
## 10. Requisitos Não Funcionais
 
- O checklist deve ser preenchível em dispositivos móveis com tela de no mínimo 5 polegadas (RNF09).
- O sistema deve salvar o progresso do checklist localmente em caso de perda de conexão.
- **RNF15** — Os registros de checklist devem ser mantidos por no mínimo 12 meses para fins de auditoria.
---
 
## 11. Ponto de Extensão
 
Não se aplica — este caso de uso é um «include» de UC05 e não possui extensões próprias.
 
---
 
## 12. Frequência de Utilização
 
**Alta** — executado a cada devolução registrada, na mesma frequência que UC05.
 
---
 
## 13. Interface Visual
 
**IV1. Tela de Checklist Técnico**
Lista de acessórios com toggles "Presente / Ausente". Lista de itens físicos com opções "OK / Danificado / N/A". Botão de câmera para captura de foto. Campo de observações livres. Botão "Concluir Checklist" no rodapé (habilitado somente após todos os itens obrigatórios serem preenchidos).
 
**IV2. Tela de Resultado do Checklist**
Exibe o resumo: itens aprovados, itens com pendência, fotos registradas e resultado final em destaque (verde = Aprovado / vermelho = Reprovado com ocorrência).
 
---
 
## 14. Observações
 
- O checklist deve ser configurável por categoria de equipamento pelo Administrador (ex.: checklist de projetor diferente do checklist de chave).
- Avaliar a inclusão de assinatura do Professor no checklist de devolução para reforçar o registro formal de ocorrências.
---
 
## 15. Referências
 
- RNF09, RNF15 — Especificação de Requisitos Não Funcionais do sistema GAC.
- RN05, RN06, RN07 — Regras de Negócio aplicáveis ao checklist e devolução.
- UC05 — Registrar Devolução de Equipamento (caso de uso chamador — «include»).
- UC09 — Enviar Notificações (acionado pelo UC05 em caso de avaria identificada).
---
 
## 16. Checklist de Validação do Artefato (CDU)
 
### 16.1 Estrutura mínima
- [x] Nome do caso de uso iniciado com verbo no infinitivo.
- [x] Objetivo claro, direto e com foco em um objetivo principal.
- [x] Tipo do caso de uso informado (abstrato).
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