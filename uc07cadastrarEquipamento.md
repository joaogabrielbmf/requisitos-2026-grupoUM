# Especificação de Requisitos Funcionais
# Caso de Uso (CDU) — UC07: Cadastrar Equipamento
 
## Histórico de Versões
 
| Data | Versão | Descrição | Autor |
|------|--------|-----------|-------|
| 14/05/2026 | 1.0 | Criação inicial do caso de uso | Equipe GAC |
 
---
 
## 1. Nome do Caso de Uso
 
Cadastrar Equipamento
 
---
 
## 2. Objetivo
 
Registrar um novo ativo no inventário do sistema GAC com todas as informações necessárias para sua identificação, rastreamento e controle de empréstimos, tornando-o disponível para uso pelos professores do CCT.
 
---
 
## 3. Tipo de Caso de Uso
 
Concreto.
 
---
 
## 4. Atores
 
### 4.1 Primário
 
**Administrador** — responsável por inserir os dados do novo equipamento no sistema e ativar o item no inventário.
 
### 4.2 Secundário
 
Não se aplica.
 
---
 
## 5. Precondições
 
- O usuário deve estar autenticado com perfil "Administrador" (UC01 concluído — RN14).
- O equipamento deve possuir etiqueta NFC ou QR Code gerada ou adquirida para ser vinculada ao cadastro.
- O equipamento não pode já estar cadastrado no sistema (número de série único).
---
 
## 6. Fluxo Principal
 
**P1. Acesso à funcionalidade de cadastro**
O Administrador acessa a seção "Inventário" no painel web e aciona o botão "Novo Equipamento". O sistema exibe o formulário de cadastro.
 
**P2. Preenchimento dos dados obrigatórios**
O Administrador preenche os campos obrigatórios: nome do equipamento, categoria (ex.: projetor, chave, cabo), marca, modelo, número de série e localização no CCT.
 
**P3. Inclusão de dados complementares**
O Administrador preenche os campos opcionais: descrição, lista de acessórios inclusos, data de aquisição, valor patrimonial e observações gerais.
 
**P4. Registro fotográfico do equipamento**
O Administrador faz o upload de uma ou mais fotos do equipamento para referência visual no sistema.
 
**P5. Vinculação do identificador físico**
O Administrador lê a etiqueta NFC ou QR Code do equipamento pelo dispositivo e o sistema vincula o identificador único ao cadastro em criação.
 
**P6. Definição do prazo padrão de devolução**
O Administrador informa o prazo padrão de devolução para a categoria do equipamento (ex.: projetor = 1 dia, chave = mesmo dia até as 22h), conforme RN08.
 
**P7. Confirmação do cadastro**
O Administrador aciona o botão "Salvar Equipamento". O sistema valida os dados, cria o registro com status inicial "Disponível" e exibe a confirmação: *"Equipamento cadastrado com sucesso. Código GAC: [código gerado]."*
 
---
 
## 7. Fluxos Alternativos
 
**A1. Cadastro de equipamento já existente (número de série duplicado)**
 
> Originado em P7, quando o sistema detecta número de série já cadastrado.
 
A1.1. O sistema exibe a mensagem: *"Já existe um equipamento cadastrado com este número de série: [código GAC]. Verifique se trata-se de um item duplicado."*
A1.2. O sistema exibe o link para o cadastro existente.
A1.3. O Administrador decide cancelar o cadastro ou corrigir o número de série informado.
A1.4. Se corrigido, o fluxo retorna ao passo P2.
 
**A2. Vinculação de identificador já utilizado**
 
> Originado em P5, quando a etiqueta NFC/QR Code lida já está vinculada a outro equipamento.
 
A2.1. O sistema exibe a mensagem: *"Este identificador já está vinculado ao equipamento [nome — código GAC]. Utilize uma etiqueta diferente."*
A2.2. O fluxo retorna ao passo P5.
 
---
 
## 8. Fluxos de Exceção
 
**E1. Campos obrigatórios não preenchidos**
 
> Originado em P7, quando o formulário é enviado com campos obrigatórios em branco.
 
E1.1. O sistema destaca os campos obrigatórios não preenchidos em vermelho.
E1.2. O sistema exibe a mensagem: *"Preencha todos os campos obrigatórios antes de salvar."*
E1.3. O fluxo retorna ao passo P2.
 
**E2. Falha no upload de imagem**
 
> Originado em P4, quando o arquivo enviado não é suportado ou excede o tamanho máximo.
 
E2.1. O sistema exibe a mensagem: *"Formato de imagem não suportado ou arquivo muito grande. Use JPG ou PNG com até 5 MB."*
E2.2. O Administrador tenta novamente ou ignora o upload e continua o cadastro sem foto.
 
**E3. Falha na leitura do identificador físico**
 
> Originado em P5, quando a leitura NFC/QR Code falha após 3 tentativas.
 
E3.1. O sistema exibe a mensagem: *"Não foi possível ler o identificador. Digite o código manualmente."*
E3.2. O sistema exibe campo de entrada manual do código da etiqueta.
E3.3. O fluxo retorna ao passo P6 após o código ser inserido.
 
---
 
## 9. Pós-condições
 
- O equipamento está registrado no inventário com status "Disponível" e código GAC único gerado.
- O identificador NFC/QR Code está vinculado ao registro do equipamento.
- O equipamento está disponível para retirada (UC03).
- O histórico de cadastro está registrado com data, hora e identificador do Administrador.
---
 
## 10. Requisitos Não Funcionais
 
- **RNF11** — O cadastro de equipamento deve ser possível via interface web em qualquer navegador moderno.
- **RNF14** — Dados de valor patrimonial devem ser tratados conforme políticas internas da Unifor.
- O código GAC gerado deve ser único e não reutilizável, mesmo após descarte do equipamento (RN13).
---
 
## 11. Ponto de Extensão
 
Não se aplica.
 
---
 
## 12. Frequência de Utilização
 
**Baixa** — ocorre pontualmente na aquisição de novos equipamentos pelo CCT, estimada em poucas vezes por mês.
 
---
 
## 13. Interface Visual
 
**IV1. Formulário de Cadastro de Equipamento (Web)**
Campos agrupados em seções: "Dados Gerais" (nome, categoria, marca, modelo, série), "Detalhes" (acessórios, data aquisição, valor), "Identificação" (leitura NFC/QR Code), "Fotos" (upload múltiplo) e "Configurações" (prazo padrão). Botões "Cancelar" e "Salvar Equipamento" no rodapé.
 
**IV2. Tela de Confirmação**
Exibe o código GAC gerado, um resumo dos dados cadastrados e botão "Ver Equipamento no Inventário".
 
---
 
## 14. Observações
 
- Avaliar integração futura com o sistema patrimonial da Unifor para importação automática de dados de novos equipamentos adquiridos.
- O prazo padrão de devolução pode ser definido por categoria, evitando a necessidade de configuração individual por equipamento.
---
 
## 15. Referências
 
- RNF11, RNF14 — Especificação de Requisitos Não Funcionais do sistema GAC.
- RN11, RN12, RN13, RN14 — Regras de Negócio: inventário e controle de acesso.
- RN08 — Regra de Negócio: prazo padrão de devolução por categoria.
- UC01 — Realizar Login (precondição — perfil Administrador).
- UC10 — Agendar Manutenção (funcionalidade complementar ao cadastro).
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