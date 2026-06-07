# Especificação de Requisitos Funcionais
# Caso de Uso (CDU) — UC01: Realizar Login
 
## Histórico de Versões
 
| Data | Versão | Descrição | Autor |
|------|--------|-----------|-------|
| 14/05/2026 | 1.0 | Criação inicial do caso de uso | Equipe GAC |
 
---
 
## 1. Nome do Caso de Uso
 
Realizar Login
 
---
 
## 2. Objetivo
 
Permitir que o usuário (Professor, Atendente ou Administrador) se autentique no sistema GAC utilizando suas credenciais institucionais, obtendo acesso às funcionalidades compatíveis com seu perfil.
 
---
 
## 3. Tipo de Caso de Uso
 
Concreto.
 
---
 
## 4. Atores
 
### 4.1 Primário
 
**Usuário** — qualquer pessoa que precise acessar o sistema (Professor, Atendente ou Administrador). O usuário inicia a interação ao acessar a tela de login.
 
### 4.2 Secundário
 
**Sistema de Autenticação Institucional (Unifor)** — valida as credenciais informadas e retorna o perfil de acesso correspondente.
 
---
 
## 5. Precondições
 
- O usuário deve possuir cadastro ativo no sistema com e-mail e senha institucionais.
- O sistema deve estar disponível e acessível via rede.
---
 
## 6. Fluxo Principal
 
**P1. Acesso à tela de login**
O usuário acessa o sistema GAC pelo navegador (web) ou pelo aplicativo mobile e o sistema exibe a tela de autenticação com os campos "E-mail" e "Senha".
 
**P2. Preenchimento das credenciais**
O usuário preenche os campos "E-mail" e "Senha" com suas credenciais institucionais.
 
**P3. Solicitação de autenticação**
O usuário aciona o botão "Entrar" e o sistema envia as credenciais ao serviço de autenticação institucional para validação.
 
**P4. Validação das credenciais**
O sistema valida as credenciais informadas e identifica o perfil de acesso do usuário (Professor, Atendente ou Administrador).
 
**P5. Redirecionamento ao painel**
O sistema redireciona o usuário ao painel inicial correspondente ao seu perfil de acesso e registra o log de entrada com data, hora e identificador do usuário.
 
---
 
## 7. Fluxos Alternativos
 
**A1. Usuário solicita redefinição de senha**
 
> Originado em P2, quando o usuário não lembra a senha.
 
A1.1. O usuário aciona o link "Esqueci minha senha".
A1.2. O sistema exibe o campo para informar o e-mail institucional.
A1.3. O usuário informa o e-mail e confirma a solicitação.
A1.4. O sistema envia um link de redefinição ao e-mail informado e exibe a mensagem: *"Um link de redefinição foi enviado para o seu e-mail institucional."*
A1.5. O fluxo é encerrado; o usuário retorna à tela de login após redefinir a senha.
 
---
 
## 8. Fluxos de Exceção
 
**E1. Credenciais inválidas**
 
> Originado em P4, quando e-mail ou senha estão incorretos.
 
E1.1. O sistema exibe a mensagem de erro: *"E-mail ou senha incorretos. Verifique suas credenciais e tente novamente."*
E1.2. Os campos "E-mail" e "Senha" são limpos.
E1.3. O sistema retorna ao passo P2.
 
**E2. Conta bloqueada por tentativas excessivas**
 
> Originado em P4, após 5 tentativas consecutivas com falha.
 
E2.1. O sistema bloqueia temporariamente o acesso da conta por 15 minutos.
E2.2. O sistema exibe a mensagem: *"Sua conta foi temporariamente bloqueada por excesso de tentativas. Tente novamente em 15 minutos ou redefina sua senha."*
E2.3. O fluxo é encerrado.
 
**E3. Sistema de autenticação indisponível**
 
> Originado em P3, quando o serviço de autenticação não responde.
 
E3.1. O sistema exibe a mensagem: *"Não foi possível conectar ao serviço de autenticação. Tente novamente em instantes."*
E3.2. O sistema retorna ao passo P2.
 
---
 
## 9. Pós-condições
 
- O usuário está autenticado e possui sessão ativa no sistema.
- O sistema registra em log: identificador do usuário, perfil, data e hora do acesso.
- O usuário visualiza apenas as funcionalidades compatíveis com seu perfil.
---
 
## 10. Requisitos Não Funcionais
 
- **RNF05** — Senhas armazenadas com hash seguro (bcrypt ou equivalente); nunca em texto puro.
- **RNF06** — A comunicação entre cliente e servidor deve ser criptografada via HTTPS/TLS 1.2+.
- A tela de login deve carregar em até 2 segundos em conexão padrão.
- Após 30 minutos de inatividade, a sessão deve ser encerrada automaticamente.
---
 
## 11. Ponto de Extensão
 
Não se aplica.
 
---
 
## 12. Frequência de Utilização
 
**Alta** — o login é realizado por todos os usuários a cada acesso ao sistema, múltiplas vezes ao dia, especialmente no início do expediente do CCT.
 
---
 
## 13. Interface Visual
 
**IV1. Tela de Login**
Campos: E-mail (texto), Senha (oculto), botão "Entrar" e link "Esqueci minha senha".
A tela é comum a todos os perfis; o redirecionamento pós-login é feito automaticamente pelo sistema conforme o perfil identificado.
 
---
 
## 14. Observações
 
- Avaliar futuramente a integração com o SSO (Single Sign-On) da Unifor para eliminar a necessidade de senha separada.
- O sistema deve registrar tentativas de login com falha para fins de auditoria de segurança.
---
 
## 15. Referências
 
- RNF05, RNF06, RNF07 — Especificação de Requisitos Não Funcionais do sistema GAC.
- RN14, RN15 — Regras de Negócio: controle de acesso por perfil.
- UC02, UC03, UC05, UC07, UC08 — demais casos de uso que dependem de autenticação prévia.
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
