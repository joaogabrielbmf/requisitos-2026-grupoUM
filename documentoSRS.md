# Especificação de Requisitos de Software (SRS) - Padrão IEEE 830
**Projeto:** GAC - Gestão de Ativos do CCT

---

## 1. Introdução

### 1.1 Propósito
O objetivo deste documento é especificar um sistema digital integrado a identificadores físicos, como NFC e/ou QR Code, para apoiar o ciclo de vida dos ativos do CCT. O sistema abrangerá todas as etapas, desde o cadastro do equipamento até a emissão de relatórios de uso. 

### 1.2 Escopo do Produto
A solução visa a substituição dos atuais controles manuais e verbais por um processo digital. O sistema proporcionará maior rastreabilidade do inventário e das movimentações de empréstimo e devolução, mitigando riscos de perda, danos sem responsabilização e sobrecarga operacional. A plataforma será composta por uma Interface Mobile para retiradas e uma Interface Web/Desktop para gestão centralizada. O escopo inclui especificação e prototipação, sem abranger o desenvolvimento completo do software.

### 1.3 Definições e Siglas
* **GAC:** Gestão de Ativos do CCT.
* **CCT:** Centro de Ciências e Tecnologia.
* **NFC / QR Code:** Tecnologias de identificação física fixadas nos equipamentos.
* **LGPD:** Lei Geral de Proteção de Dados.
* **RBAC:** *Role-Based Access Control* (Controle de Acesso Baseado em Perfis).

### 1.4 Visão Geral do Documento
Este documento está dividido em três seções principais. A Seção 2 apresenta uma descrição geral do sistema, seus usuários e restrições. A Seção 3 detalha os requisitos funcionais, não funcionais, regras de negócio e interfaces que guiarão a validação do projeto.

---

## 2. Descrição Geral

### 2.1 Perspectiva do Produto
O sistema GAC atua como uma solução de duas pontas complementares:
* **Interface Mobile:** Utilizada nos smartphones dos professores para acessos ágeis na ponta.
* **Interface Web/Desktop:** Utilizada nos computadores da recepção para controle de inventário e emissão de relatórios.
* O sistema prevê potencial integração futura com os sistemas de TI da Unifor para unificação de dados.

### 2.2 Características dos Usuários (Personas)
* **Professor do CCT:** Docente que utiliza a aplicação móvel exclusivamente para retirar e devolver equipamentos de forma ágil.
* **Atendente / Equipe do CCT:** Funcionário que opera a recepção, controlando rotinas de devoluções e executando checklists técnicos.
* **Administrador / Coordenação:** Perfil de gestão que possui privilégios para gerenciar o inventário completo, cadastrar novos equipamentos e gerar relatórios estratégicos na Interface Web.

### 2.3 Restrições e Suposições
* A infraestrutura de rede (Wi-Fi corporativo) deve ter cobertura e estabilidade no ambiente do CCT.
* O armazenamento da aplicação móvel instalada nos smartphones não pode ultrapassar 50 MB.
* O tratamento de dados deve seguir rigorosamente as diretrizes da LGPD e as políticas da instituição.

---

## 3. Requisitos Específicos

### 3.1 Regras de Negócio (RN)
As regras de negócio ditam as lógicas obrigatóricas que o sistema e os usuários devem obedecer durante a operação.

* **RN01 - Aceite do Termo de Responsabilidade:** Para realizar a retirada de um equipamento via mobile, o professor deve fornecer o aceite digital explícito do Termo de Responsabilidade após a leitura do NFC/QR Code. Sem este aceite, o empréstimo não pode ser concluído.
* **RN02 - Cancelamento por Time-out:** Se uma operação de empréstimo iniciada via etiqueta ficar travada ou não receber a assinatura digital em até 5 minutos, a transação deve expirar e o ativo deve retornar automaticamente para o estado "Disponível".
* **RN03 - Preenchimento de Checklist Obrigatório:** A rotina de devolução na Interface Web não pode ser concluída sem que o atendente/administrador marque todos os itens obrigatórios do checklist técnico (ex: estado físico geral, presença de cabos/controles).
* **RN04 - Bloqueio por Avaria Grave:** Se o checklist técnico de devolução apontar avaria grave, o sistema deve alterar o status do ativo para "Em Manutenção", impedindo novas tentativas de empréstimo até a liberação manual por um administrador.
* **RN05 - Restrição Baseada em Perfis (RBAC):** O controle de acesso deve restringir permissões e telas apresentadas: Professores acessam apenas retiradas via mobile; Atendentes operam devoluções e checklists; Administradores gerenciam inventário, cadastros e relatórios.

### 3.2 Requisitos Funcionais
Esta seção descreve as funcionalidades ativas do sistema, baseadas nos Casos de Uso (UC) e integradas às Regras de Negócio (RN).

* **RF01 - Realizar Login (UC01):** O sistema deve permitir que o usuário se autentique utilizando credenciais institucionais, restringindo as funcionalidades baseadas em seu perfil conforme a **RN05**.
* **RF02 - Consultar Disponibilidade (UC02):** O sistema deve permitir a verificação, em tempo real, do status de um equipamento no inventário, oferecendo filtros e exibindo dados como acessórios e fotos.
* **RF03 - Registrar Retirada (UC03):** O sistema deve registrar a saída de equipamentos através da leitura de NFC ou QR Code. O fluxo deve obedecer à **RN02**, cancelando operações inativas por mais de 5 minutos.
* **RF04 - Assinar Termo Digital (UC04):** O sistema deve exigir e registrar o aceite formal do Termo de Responsabilidade pelo professor como condição obrigatória para a retirada, cumprindo a **RN01**.
* **RF05 - Registrar Devolução (UC05):** O sistema deve formalizar o retorno do item ao CCT, identificando a retirada vinculada e atualizando o status para "Disponível" apenas após a conclusão do checklist.
* **RF06 - Realizar Checklist Técnico (UC06):** Integrado à devolução, o sistema deve fornecer um formulário de conferência obrigatória (**RN03**). Em caso de detecção de danos severos, o sistema deve bloquear o equipamento com o status "Em Manutenção" (**RN04**).
* **RF07 - Cadastrar Equipamento (UC07):** O sistema deve permitir ao Administrador registrar novos ativos no inventário, vinculando o código de série e a etiqueta física (NFC/QR Code).
* **RF08 - Gerar Relatórios (UC08):** O sistema deve fornecer aos Administradores painéis analíticos com dados de retiradas, ocorrências e inventário geral, permitindo exportação em formatos PDF e CSV.
* **RF09 - Enviar Notificações (UC09):** O sistema deve gerar e disparar alertas e notificações automáticas, incluindo lembretes de devolução próxima ao prazo para os professores e alertas de atraso ou detecção de avarias para a equipe administrativa.
* **RF10 - Agendar e Gerenciar Manutenção (UC10):** O sistema deve permitir o agendamento de manutenções preventivas, o registro de manutenções corretivas derivadas de checklists com avarias e o acompanhamento do status do ativo até sua liberação de volta para o status "Disponível".

### 3.3 Requisitos Não Funcionais
Atributos de qualidade, segurança e desempenho do sistema.

#### 3.3.1 Desempenho e Eficiência
* O aplicativo mobile deve processar a leitura da etiqueta e carregar a tela em até 2 segundos sob conexão local.
* A atualização de status no banco de dados, após validação de devolução, deve ocorrer com limite máximo de 3 segundos.
* O sistema deve suportar picos de acessos simultâneos sem degradação durante horários de troca de turno.

#### 3.3.2 Segurança e Privacidade
* A comunicação de dados entre cliente e servidor deve ser criptografada por protocolo HTTPS/TLS.
* Campos de cadastro e leituras de QR Code devem possuir sanitização para prevenir ataques de injeção de dados.
* Os registros de empréstimos, checklists e assinaturas devem ser imutáveis para fins de auditoria.
* Apenas dados estritamente necessários para a responsabilização patrimonial devem ser coletados e armazenados.

#### 3.3.3 Usabilidade e Acessibilidade
* O fluxo de retirada via mobile deve permitir a primeira operação em menos de 1 minuto, sem exigir treinamento.
* As interfaces devem seguir diretrizes de acessibilidade (WCAG), oferecendo compatibilidade com leitores de tela e contraste adequado.
* A interface Desktop na recepção deve contar com atalhos de teclado para otimizar o fluxo de atendimento.

#### 3.3.4 Confiabilidade e Tolerância a Falhas
* O sistema deve garantir disponibilidade mínima de 99,5% entre segunda e sábado, das 07:00 às 22:30.
* Em caso de perda temporária de rede, o aplicativo deve reter dados localmente e sincronizá-los após o restabelecimento da conexão.
* O sistema deve possuir rotinas diárias automatizadas de backup com Tempo de Recuperação (RTO) inferior a 4 horas.

### 3.4 Interfaces Externas
* **Integração Unifor:** O backend deverá utilizar APIs RESTful seguras para comunicação com sistemas de TI institucionais, validando a matrícula e o vínculo funcional de professores e funcionários. Em caso de falha desta API, o sistema deve operar localmente utilizando dados de cache.
