# Especificação de Requisitos Não Funcionais

## Histórico de Versões

| Data       | Versão | Descrição                                                          | Autor                                          |
| ---------- | ------- | -------------------------------------------------------------------- | ---------------------------------------------- |
| 19/05/2026 | 1.0     | Elaboração inicial dos RNFs baseada no Documento de Visão do GAC. | Disciplina: Requisitos e Modelagem de Sistemas |

## 1. Requisitos de Produto

### 1.1. Eficiência de Desempenho

#### 1.1.1. Comportamento temporal

* **RNF-01 (Tempo de Leitura NFC/QR Code):** O aplicativo mobile deve processar a leitura da etiqueta física (NFC ou QR Code) fixada no ativo e exibir a tela com as informações e o Termo de Responsabilidade em até 2 segundos sob conexão Wi-Fi/4G local.
* **RNF-02 (Tempo de Sincronização):** A atualização do status do equipamento para "Disponível" no banco de dados, após o checklist de devolução na Interface Web, deve ocorrer em tempo real (limite máximo de 3 segundos).

#### 1.1.2. Capacidade

* **RNF-03 (Acessos Simultâneos):** A infraestrutura do sistema deve suportar picos de acessos simultâneos de professores realizando retiradas nos horários de troca de turno de aulas (ex.: janelas de 15 minutos antes e depois do início das aulas) sem degradação do tempo de resposta.

#### 1.1.3. Uso de recursos

* **RNF-04 (Consumo de Armazenamento Mobile):** Sendo um aplicativo focado em rotinas rápidas de campo, a aplicação móvel instalada nos smartphones dos professores deve ocupar no máximo 50 MB de armazenamento interno (excluindo cache de dados temporários).

### 1.2. Flexibilidade (portabilidade)

#### 1.2.1. Escalabilidade

* **RNF-05 (Volume do Inventário):** A arquitetura do banco de dados deve ser projetada para suportar o crescimento do inventário de ativos do CCT (chaves, projetores, adaptadores) em até 500% sem perda de performance nas consultas e relatórios.

#### 1.2.2. Adaptabilidade

* **RNF-06 (Multiplataforma Web):** A Interface Web/Desktop operada pela equipe da recepção e coordenação deve ser responsiva e totalmente funcional nos principais navegadores do mercado (Google Chrome, Mozilla Firefox, Microsoft Edge e Safari).

#### 1.2.3. Instalabilidade

* **RNF-07 (Distribuição Mobile):** O aplicativo mobile para os professores deve estar disponível para download nas lojas oficiais (Google Play Store e Apple App Store) ou via distribuição homologada pela TI da Unifor.

#### 1.2.4. Substituibilidade

* **RNF-08 (Troca de Tecnologia de Captura):** O módulo de leitura do aplicativo deve ser modular para permitir a substituição ou alternância transparente entre a leitura de QR Code e tags NFC, utilizando a mesma interface lógica de validação do ativo.

### 1.3. Confiabilidade

#### 1.3.1. Maturidade

* **RNF-09 (Taxa de Erro na Identificação):** O algoritmo de decodificação de QR Codes/NFC deve apresentar uma taxa de falha de leitura menor que 1% em ambientes com iluminação padrão das salas e recepção do CCT.

#### 1.3.2. Disponibilidade

* **RNF-10 (Tempo de Atividade):** Os serviços de backend e banco de dados do GAC devem operar com disponibilidade mínima de 99,5% durante os horários de funcionamento letivo do CCT (segunda a sábado, das 07:00 às 22:30).

#### 1.3.3. Tolerância a falhas

* **RNF-11 (Operação em Instabilidade de Rede):** Caso o smartphone do professor perca conectividade temporária durante o checklist inicial, o aplicativo deve reter os dados coletados localmente e tentar reenviar a requisição assim que a conexão com a rede Unifor for restabelecida.

#### 1.3.4. Recuperabilidade

* **RNF-12 (Rotina de Backup):** O sistema deve prever políticas de backup automatizadas diárias para o histórico de movimentações, auditorias e cadastros de inventário, garantindo um RTO (Tempo de Recuperação) menor que 4 hours em caso de falha crítica do servidor.

### 1.4. Segurança

#### 1.4.1. Confidencialidade

* **RNF-13 (Criptografia de Dados):** Todo o tráfego de dados entre as interfaces (Mobile e Web) e o servidor de backend deve ser criptografado via protocolo HTTPS/TLS. Dados sensíveis de professores e servidores não devem ficar expostos.

#### 1.4.2. Integridade

* **RNF-14 (Imutabilidade do Histórico):** Os registros de empréstimos consolidados, assinaturas de termos e checklists técnicos concluídos não podem ser editados ou apagados diretamente pelos usuários, garantindo a integridade em auditorias futuras.

#### 1.4.3. Não repúdio

* **RNF-15 (Aceite Digital do Termo):** A retirada rápida via mobile exige o aceite digital explícito do Termo de Responsabilidade vinculado à identidade autenticada do professor, impedindo a negação da autoria da retirada.

#### 1.4.4. Autenticidade (autenticação)

* **RNF-16 (Controle de Acesso Baseado em Perfis - RBAC):** O sistema deve validar as identidades e restringir as telas por perfil: Professores acessam apenas a interface mobile de retirada; Atendentes operam devoluções/checklists; Administradores gerenciam inventário e relatórios.

#### 1.4.5. Resistência

* **RNF-17 (Proteção Contra Injeção de Dados):** Os campos de cadastro de novos equipamentos na Interface Web e os payloads enviados via leitura de QR Code devem passar por camadas de sanitização para evitar ataques de SQL Injection e Cross-Site Scripting (XSS).

### 1.5. Privacidade

#### 1.5.1. Licitude

* **RNF-18 (Conformidade LGPD):** O armazenamento e tratamento dos dados de identificação dos professores e funcionários do CCT devem seguir estritamente as diretrizes da Lei Geral de Proteção de Dados (LGPD) e as políticas internas de TI da Unifor.

#### 1.5.2. Finalidade

* **RNF-19 (Restrição de Escopo dos Dados):** Os dados funcionais coletados (matrícula, nome, vínculo institucional) possuem a finalidade exclusiva de responsabilização patrimonial pelo uso de ativos do CCT.

#### 1.5.3. Necessidade

* **RNF-20 (Minimização de Dados):** O sistema deve coletar apenas o estritamente necessário para a operação. Informações pessoais externas à relação institucional do professor com o CCT não devem ser requisitadas ou armazenadas.

#### 1.5.4. Tratamento

* **RNF-21 (Ciclo de Vida do Dado):** Os logs de movimentação de empréstimos devem permanecer arquivados para fins de auditoria e relatórios gerenciais pelo tempo determinado pelas normas de controle patrimonial da instituição, sendo anonimizados após o período de retenção legal.

### 1.6. Capacidade de Interação (UX, usabilidade e acessibilidade)

#### 1.6.1. Reconhecimento de adequação

* **RNF-22 (Identidade Visual):** O layout e a navegação das interfaces devem deixar explícito o propósito de gestão de ativos, exibindo alertas visuais claros sobre pendências de devolução e o status atualizado de cada item consultado.

#### 1.6.2. Facilidade de aprendizado (learnability)

* **RNF-23 (Intuitividade da Retirada):** O fluxo de retirada rápida via mobile pelo professor (Ler Código -> Validar Item -> Aceitar Termo) deve ser projetado para que o usuário consiga concluir a primeira operação em menos de 1 minuto sem necessidade de treinamento prévio.

#### 1.6.3. Operabilidade

* **RNF-24 (Eficiência na Recepção):** A Interface Web/Desktop deve priorizar atalhos de teclado e fluxos otimizados na recepção para reduzir o retrabalho operacional dos atendentes durante os horários de pico.

#### 1.6.4. Proteção contra erros do usuário

* **RNF-25 (Validação de Checklist):** A Interface Web deve impedir a conclusão da rotina de devolução sem que todos os itens obrigatórios do checklist técnico (ex.: presença de cabos, controle remoto, estado físico) estejam marcados.

#### 1.6.5. Inclusividade (acessibilidade)

* **RNF-26 (Acessibilidade de Interface):** As interfaces Web e Mobile devem seguir as diretrizes básicas de acessibilidade (como as WCAG), oferecendo contraste adequado e compatibilidade com leitores de tela nativos de smartphones e desktops.

#### 1.6.6. Assistência ao usuário (acessibilidade)

* **RNF-27 (Mensagens de Erro Instrucionais):** Diante de erros operacionais (ex: etiqueta corrompida ou inacessível), o sistema deve apresentar mensagens instrucionais claras informando o que o usuário deve fazer ("Por favor, digite o código numérico do ativo ou procure o atendente da recepção").

#### 1.6.7. Engajamento do usuário

* **RNF-28 (Satisfação Visual):** O design das telas deve ser limpo e moderno, diminuindo a sobrecarga cognitiva do funcionário e garantindo uma experiência fluida para o professor na ponta.

### 1.7. Manutenibilidade

#### 1.7.1. Modularidade

* **RNF-29 (Desacoplamento de Módulos):** O módulo responsável pelo envio de notificações e alertas automáticos deve ser desacoplado do módulo principal de empréstimos, permitindo manutenções e alterações de canais (E-mail, SMS, Push) sem impactar as regras de negócio de retirada.

#### 1.7.2. Reusabilidade

* **RNF-30 (Componentização de UI):** Os componentes de interface de usuário utilizados no checklist técnico e na listagem de inventário devem ser reaproveitados entre as visualizações de atendentes e coordenadores.

#### 1.7.3. Analisabilidade

* **RNF-31 (Rastreamento de Erros/Logs):** O backend do sistema deve implementar rotinas de geração de logs de erro estruturados para facilitar a identificação rápida e o diagnóstico de falhas em chamadas de API ou integrações.

#### 1.7.4. Modificabilidade

* **RNF-32 (Facilidade de Evolution):** A arquitetura do banco de dados e do código deve permitir a inserção de novos campos de checklist técnicos ou novos tipos de ativos com impacto nulo na base de dados histórica existente.

#### 1.7.5. Testabilidade

* **RNF-33 (Ambiente Isolado de Homologação):** Toda a lógica especificada deve viabilizar a criação de cenários de testes automatizados unitários e de integração para validar as regras críticas de negócio (como a regra de não permitir empréstimo duplo do mesmo item simultaneamente).

### 1.8. Compatibilidade

#### 1.8.1. Interoperabilidade

* **RNF-34 (Integração com Sistemas Unifor):** O backend do GAC deve ser planejado para interagir de forma segura através de APIs RESTful com os sistemas institucionais de TI da Unifor para fins de validação de matrículas/vínculos de professores e funcionários.

#### 1.8.2. Coexistência

* **RNF-35 (Uso de Recursos Compartilhados):** A aplicação móvel deve coexistir e operar sem conflitos com outros aplicativos corporativos e acadêmicos já instalados nos aparelhos dos docentes.

### 1.9. Segurança Operacional (safety)

#### 1.9.1. Restrição operacional

* **RNF-36 (Bloqueio de Ativo Danificado):** Caso o checklist técnico aponte avaria grave, o sistema deve restringir operacionalmente o status do ativo para "Em Manutenção", impedindo automaticamente novas tentativas de empréstimo via mobile até a liberação do administrador.

#### 1.9.2. Identificação de riscos

* **RNF-37 (Sinalização de Equipamentos Críticos):** O painel do administrador deve identificar visualmente e com alta prioridade ativos que estejam retidos além do prazo regulamentar, indicando risco de perda patrimonial ou desfalque para as próximas aulas.

#### 1.9.3. Segurança contra falhas (fail-safe)

* **RNF-38 (Cancelamento por Time-out):** Se uma operação de empréstimo iniciada via QR Code/NFC ficar travada ou não for assinada digitalmente pelo professor em até 5 minutos, a transação deve expirar e o ativo deve voltar ao estado "Disponível" para evitar travamentos no fluxo.

#### 1.9.4. Aviso de perigo

* **RNF-39 (Alertas de Manutenção Preventiva):** O sistema deve emitir avisos preventivos para os administradores quando um ativo atingir o número máximo estipulado de horas de uso ou empréstimos contínuos, mitigando falhas técnicas repentinas durante as aulas.

#### 1.9.5. Integração segura

* **RNF-40 (Isolamento de Falhas de API):** Se o módulo de integração externa com a Unifor estiver fora do ar, o GAC deve operar em modo de contingência local baseando-se no último cache de dados válidos, sem interromper as retiradas essenciais do CCT.

### 1.10. Adequação funcional

#### 1.10.1. Completude funcional

* **RNF-41 (Alinhamento com o Escopo):** O escopo de especificação e prototipagem deve contemplar todas as fases do ciclo de vida dos ativos descritos no objetivo da demanda: cadastro de inventário, fluxo de empréstimo móvel, devolução com checklist técnico e relatórios gerenciais.

#### 1.10.2. Corretude funcional

* **RNF-42 (Precisão do Histórico):** Os relatórios estratégicos emitidos pela Interface Web/Desktop devem apresentar dados exatos sobre a taxa de ocupação, tempo de posse e histórico de danos dos equipamentos, batendo integralmente com as transações salvas.

#### 1.10.3. Adequação funcional

* **RNF-43 (Eficácia de Processo):** O ecossistema composto pelas interfaces mobile e desktop deve efetivamente mitigar a ausência de registro formal de empréstimos anteriores e diminuir sensivelmente o tempo gasto na conferência manual de itens na recepção.

## 2. Requisitos Externos

### 2.1. Ético

* **RNF-44 (Transparência de Uso):** O Termo de Responsabilidade exibido na Interface Mobile deve esclarecer de forma transparente as responsabilidades atribuídas ao professor, as métricas de uso registradas e a forma como seus dados corporativos são expostos na plataforma de auditoria do CCT.

### 2.2. Regulatório

* **RNF-45 (Políticas Patrimoniais da Instituição):** As regras de negócio implementadas (ex.: tempos de devolução permitidos, prioridades de agendamento de manutenção) devem estar em total conformidade com os regulamentos internos de controle e inventário de bens móveis adotados pela instituição acadêmica.

### 2.3. Legislativo

* **RNF-46 (Adesão Legal):** Como o sistema gerencia dados de servidores, docentes e patrimônio físico, o desenho de sua arquitetura de dados e armazenamento deve submeter-se às legislações federais e estaduais aplicáveis ao tratamento de informações institucionais no Brasil.

## 3. Requisitos Organizacionais

### 3.1. Ambientais

* **RNF-47 (Ambiente Operacional das Interfaces):** A solução móvel será operada nos blocos e salas de aula do CCT pelos professores em seus dispositivos pessoais. A interface gerencial será executada a partir dos computadores desktop situados na recepção e salas administrativas do CCT.

### 3.2. Operacionais

* **RNF-48 (Infraestrutura de Rede Local):** O funcionamento contínuo do sistema pressupõe a cobertura e estabilidade da rede de conectividade sem fio (Wi-Fi corporativo) presente em todo o ambiente geográfico do CCT.

### 3.3. Desenvolvimento

* **RNF-49 (Restrições do Projeto de Extensão):** Os entregáveis obrigatórios deste projeto limitam-se à criação da documentação de engenharia de requisitos (Modelagem UML: Casos de Uso, Componentes e Implantação) e o desenvolvimento de protótipos funcionais de interface de usuário (UI/UX). O desenvolvimento completo do código do software (coding) está fora do escopo desta etapa.

## 4. Checklist de Validação do Artefato (RNF)

### 4.1. Estrutura e escopo

* [ ] O documento possui histórico de versões preenchido.
* [ ] O escopo da solução está claro no documento.
* [ ] Há requisitos registrados nas seções aplicáveis (produto, externos e organizacionais).
* [ ] Requisitos não aplicáveis estão explicitamente marcados como "Não se aplica", quando necessário.

### 4.2. Qualidade dos requisitos

* [ ] Cada requisito está escrito de forma objetiva e verificável.
* [ ] Cada requisito possui critério mensurável (tempo, percentual, limite, condição ou evidência).
* [ ] Não há requisito ambíguo com termos vagos (ex.: "rápido", "seguro", "fácil") sem métrica.
* [ ] Requisitos duplicados ou conflitantes foram eliminados.

### 4.3. Conformidade e rastreabilidade

* [ ] Requisitos regulatórios/legais relevantes foram registrados.
* [ ] Requisitos de privacidade e segurança foram contemplados quando aplicáveis.
* [ ] Os requisitos estão alinhados com visão da demanda, glossário e casos de uso.
* [ ] Existe rastreabilidade dos requisitos para fontes de negócio, norma ou decisão técnica.

### 4.4. Prontidão para uso

* [ ] Os requisitos podem ser usados como base para implementação e testes.
* [ ] Há insumos suficientes para criar critérios de aceitação.
* [ ] O documento foi revisado por pares.
* [ ] A versão está pronta para aprovação/publicação.
