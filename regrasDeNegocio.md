# Regras de Negócio da Solução (RN) - GAC

## 1. Regras de Negócio

### RN01
* **Identificador:** RN01 - Professores devem aceitar o Termo de Responsabilidade.
* **Descrição:** Para realizar a retirada ágil de um equipamento via mobile, o professor deve fornecer o aceite digital explícito do Termo de Responsabilidade após a identificação do ativo por leitura de NFC ou QR Code. Sem o registro deste aceite vinculado à identidade autenticada do professor, o sistema não deve permitir a conclusão do empréstimo.

### RN02
* **Identificador:** RN02 - Sistema deve cancelar empréstimos inativos por time-out.
* **Descrição:** Se uma operação de empréstimo iniciada via leitura de etiqueta (QR Code ou NFC) ficar travada ou não receber a assinatura digital do professor no prazo de 5 minutos, a transação deve expirar. O sistema deve, então, retornar o ativo automaticamente para o estado "Disponível" a fim de evitar travamentos no fluxo operacional.

### RN03
* **Identificador:** RN03 - Operadores devem preencher checklist técnico obrigatório na devolução.
* **Descrição:** O sistema deve impedir que a rotina de devolução seja concluída na Interface Web sem que o atendente ou administrador marque todos os itens obrigatórios exigidos no checklist técnico. O checklist inclui validações como estado físico geral e presença de cabos e controles remotos.

### RN04
* **Identificador:** RN04 - Sistema deve bloquear ativos identificados com avaria grave.
* **Descrição:** Caso a conferência de acessórios e estado físico durante o checklist técnico de devolução aponte avaria grave, o sistema deve alterar o status do ativo restritamente para "Em Manutenção". Este status impedirá novas tentativas de empréstimo do item via aplicativo mobile até que ocorra a liberação manual por um administrador.

### RN05
* **Identificador:** RN05 - Sistema deve restringir funcionalidades baseado em perfis (RBAC).
* **Descrição:** O controle de acesso da plataforma deve restringir as permissões e telas apresentadas de acordo com o papel do usuário. Os professores têm acesso apenas à interface mobile para realizar retiradas. Os atendentes operam as rotinas de devoluções e checklists técnicos. Já os administradores e coordenação possuem privilégios para gerenciar o inventário completo, cadastrar novos equipamentos e gerar relatórios estratégicos na Interface Web.

---

## 2. Checklist de Validação das Regras de Negócio

As regras acima foram elaboradas e validadas seguindo os critérios do modelo LAPIS:

### 2.1 Estrutura mínima
* [ ] Identificador único e padronizado.
* [ ] Nome da regra no formato sujeito + verbo + objeto.
* [ ] Descrição clara, direta e sem ambiguidades.

### 2.2 Qualidade da regra
* [ ] A regra descreve apenas uma decisão/comportamento principal.
* [ ] Condições de aplicação (gatilho/contexto) estão explícitas.
* [ ] Resultado esperado da regra está explícito.
* [ ] A regra é verificável e testável.

### 2.3 Consistência e rastreabilidade
* [ ] Não há conflito com outras regras já existentes.
* [ ] A regra referencia origem (negócio, norma, lei ou decisão do cliente), quando aplicável.
* [ ] A regra está alinhada com CDU, RNF e demais artefatos relacionados.

### 2.4 Prontidão
* [ ] Conteúdo revisado por pares.
* [ ] Regra pronta para uso em análise, desenvolvimento e testes.
