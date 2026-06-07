# Especificação de Requisitos Funcionais
# Caso de Uso (CDU) — UC04: Assinar Termo Digital de Responsabilidade
 
## Histórico de Versões
 
| Data | Versão | Descrição | Autor |
|------|--------|-----------|-------|
| 14/05/2026 | 1.0 | Criação inicial do caso de uso | Equipe GAC |
 
---
 
## 1. Nome do Caso de Uso
 
Assinar Termo Digital de Responsabilidade
 
---
 
## 2. Objetivo
 
Registrar o aceite formal e digital do Professor ao Termo de Responsabilidade pelo uso do equipamento retirado, garantindo o vínculo legal entre o usuário e o item emprestado como condição obrigatória para conclusão da retirada.
 
---
 
## 3. Tipo de Caso de Uso
 
Abstrato — é sempre invocado por UC03 (Registrar Retirada de Equipamento) por meio de relacionamento «include», nunca iniciado diretamente pelo ator.
 
---
 
## 4. Atores
 
### 4.1 Primário
 
**Professor** — lê e aceita o Termo de Responsabilidade digitalmente, formalizando a responsabilidade sobre o equipamento.
 
### 4.2 Secundário
 
Não se aplica.
 
---
 
## 5. Precondições
 
- O caso de uso UC03 — Registrar Retirada deve estar em execução (passo P5).
- O equipamento identificado deve estar validado e com status "Disponível".
- O Professor deve estar autenticado no sistema (UC01 concluído).
---
 
## 6. Fluxo Principal
 
**P1. Exibição do Termo de Responsabilidade**
O sistema exibe o Termo de Responsabilidade completo na tela, contendo: identificação do Professor, dados do equipamento (nome, código, acessórios), data/hora da retirada, prazo de devolução e as responsabilidades do usuário pelo item.
 
**P2. Leitura do termo pelo Professor**
O Professor rola o conteúdo do termo até o final; o sistema habilita os botões de ação apenas após o termo ter sido rolado integralmente.
 
**P3. Aceite do Termo**
O Professor aciona o botão "Li e Aceito os Termos" e o sistema registra o aceite com: identificador do Professor, data, hora e versão do termo aceito.
 
**P4. Confirmação e retorno ao fluxo chamador**
O sistema exibe brevemente a mensagem: *"Termo assinado com sucesso."* e retorna ao UC03 para conclusão do registro de retirada (passo P6).
 
---
 
## 7. Fluxos Alternativos
 
**A1. Professor solicita envio do termo por e-mail**
 
> Originado em P1, quando o Professor deseja uma cópia para seus registros.
 
A1.1. O Professor aciona o botão "Enviar cópia por e-mail".
A1.2. O sistema envia uma cópia do termo em PDF para o e-mail institucional do Professor.
A1.3. O sistema exibe a mensagem: *"Uma cópia do termo foi enviada para o seu e-mail."*
A1.4. O fluxo retorna ao passo P2.
 
---
 
## 8. Fluxos de Exceção
 
**E1. Professor recusa o termo**
 
> Originado em P3, quando o Professor aciona o botão "Recusar".
 
E1.1. O sistema exibe a mensagem de confirmação: *"Ao recusar, a retirada será cancelada. Deseja continuar?"*
E1.2. O Professor confirma a recusa.
E1.3. O sistema cancela o processo de retirada, mantém o status do equipamento como "Disponível" e retorna ao UC03 indicando cancelamento.
E1.4. O UC03 é encerrado sem registrar retirada.
 
**E2. Tempo de sessão expirado durante leitura do termo**
 
> Originado em P2, quando o Professor demora mais de 10 minutos na tela do termo.
 
E2.1. O sistema exibe o aviso: *"Sua sessão está prestes a expirar. Deseja continuar?"*
E2.2. Se o Professor confirmar, o sistema renova a sessão e o fluxo retorna ao passo P2.
E2.3. Se o Professor não responder em 2 minutos, a sessão é encerrada, o processo de retirada é cancelado e o equipamento permanece disponível.
 
---
 
## 9. Pós-condições
 
- O aceite do Professor está registrado no sistema com data, hora e versão do termo.
- O registro do aceite é vinculado à retirada e ao histórico do Professor.
- O fluxo retorna ao UC03 habilitando a conclusão da retirada.
---
 
## 10. Requisitos Não Funcionais
 
- **RNF06** — A transmissão do termo e do registro de aceite deve ocorrer via HTTPS/TLS 1.2+.
- O aceite deve ser armazenado com registro de data/hora e não pode ser alterado após confirmação.
- **RNF15** — O histórico de aceites de termos deve ser mantido por no mínimo 12 meses para fins de auditoria.
---
 
## 11. Ponto de Extensão
 
Não se aplica — este caso de uso é um «include» de UC03 e não possui extensões próprias.
 
---
 
## 12. Frequência de Utilização
 
**Alta** — é executado a cada retirada registrada, na mesma frequência que UC03.
 
---
 
## 13. Interface Visual
 
**IV1. Tela do Termo de Responsabilidade**
Área de rolagem com o texto completo do termo. Botão "Enviar cópia por e-mail" no topo. Botões "Recusar" (secundário) e "Li e Aceito os Termos" (primário, desabilitado até rolagem completa) no rodapé. Os dados do equipamento e do Professor são exibidos em destaque no cabeçalho do termo.
 
---
 
## 14. Observações
 
- O texto do Termo de Responsabilidade deve ser elaborado em conjunto com a equipe jurídica ou de compliance da Unifor antes da implantação.
- A versão do termo aceito deve ser registrada para rastreabilidade em caso de atualização do documento.
---
 
## 15. Referências
 
- RNF06, RNF15 — Especificação de Requisitos Não Funcionais do sistema GAC.
- RN02 — Regra de Negócio: retirada exige assinatura digital do Termo de Responsabilidade.
- UC03 — Registrar Retirada de Equipamento (caso de uso chamador — «include»).
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