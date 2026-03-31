# Guia de Estudo: AWS Certified Developer - Associate (DVA-C02)

Este guia foi estruturado para auxiliar no aprendizado ativo e na preparação técnica para a certificação **AWS Certified Developer Associate**, focando nos conceitos fundamentais, serviços essenciais e práticas de exame.

---

### 1. CONTEXTO E OBJETIVO

A certificação **AWS Certified Developer - Associate (DVA-C02)** é destinada a indivíduos que desempenham uma função de desenvolvedor e valida a proficiência na criação, teste, implantação e depuração de aplicações baseadas na nuvem AWS. O exame exige que o candidato tenha, idealmente, um ou mais anos de experiência prática no desenvolvimento e manutenção de aplicações AWS.

**Principais Tópicos Cobrados (Domínios):**
*   **Desenvolvimento com Serviços AWS (32%):** Escrita de código, uso de SDKs e armazenamento de dados.
*   **Segurança (26%):** Autenticação, autorização, criptografia e gerenciamento de dados sensíveis.
*   **Implantação (24%):** Estratégias de CI/CD, preparação de artefatos e testes automatizados.
*   **Solução de Problemas e Otimização (18%):** Análise de causa raiz, observabilidade e instrumentação de código.

**Objetivos de Estudo:**
1.  Dominar o uso de **SDKs da AWS** para interagir programaticamente com serviços.
2.  Entender profundamente arquiteturas **Serverless** (Lambda, API Gateway, DynamoDB).
3.  Implementar práticas de **segurança** utilizando IAM e Cognito.
4.  Aprender estratégias de **monitoramento e tracing** para otimização de performance.

---

### 2. RESUMO ESTRUTURADO DOS SERVIÇOS

#### **IAM (Identity and Access Management)**
*   **Definição:** Serviço que ajuda a controlar com segurança o acesso aos recursos da AWS.
*   **Como funciona:** Gerencia usuários, grupos e funções (Roles), permitindo ou negando permissões através de políticas (JSON).
*   **Caso de uso real:** Atribuir uma **Role** a uma instância EC2 ou função Lambda para que ela possa ler objetos de um bucket S3 sem precisar de chaves de acesso fixas no código.
*   **Dicas para prova:** Foque no princípio do privilégio mínimo e no uso de **Access Keys/Secret Keys** apenas para acesso programático local.

#### **AWS Lambda**
*   **Definição:** Serviço de computação serverless que executa código em resposta a eventos sem gerenciar servidores.
*   **Como funciona:** O código é disparado por eventos de outros serviços (como S3 ou DynamoDB) e escala automaticamente.
*   **Caso de uso real:** Processar e redimensionar imagens automaticamente assim que são enviadas para um bucket S3.
*   **Dicas para prova:** Entenda a **simultaneidade provisionada** para evitar problemas de "cold start" (inicialização lenta).

#### **Amazon API Gateway**
*   **Definição:** Serviço totalmente gerenciado que facilita a criação, publicação e proteção de APIs em qualquer escala.
*   **Como funciona:** Atua como uma "porta de entrada" para aplicações acessarem dados ou lógica de negócios em serviços de backend (como Lambda ou EC2).
*   **Caso de uso real:** Expor uma função Lambda como um endpoint HTTP RESTful para ser consumido por um aplicativo móvel.
*   **Dicas para prova:** Estude a diferença entre APIs REST e HTTP, e o uso de **implantações canário** para lançar alterações com segurança.

#### **Amazon DynamoDB**
*   **Definição:** Banco de dados NoSQL chave-valor, serverless, com performance de milissegundos em qualquer escala.
*   **Como funciona:** Armazena dados em tabelas sem esquema fixo, utilizando Chaves de Partição e de Classificação para indexação.
*   **Caso de uso real:** Armazenar o estado de carrinhos de compras de milhões de usuários simultâneos com latência consistente.
*   **Dicas para prova:** Conheça os **Índices Secundários Globais (GSI)** para flexibilidade em consultas por atributos que não são a chave primária.

#### **Amazon S3 (Simple Storage Service)**
*   **Definição:** Serviço de armazenamento de objetos escalável, altamente disponível e durável.
*   **Como funciona:** Os dados são armazenados como objetos dentro de recipientes chamados buckets.
*   **Caso de uso real:** Hospedagem de sites estáticos ou armazenamento de backups de logs de aplicação.
*   **Dicas para prova:** Use **URLs pré-assinadas** para permitir que usuários façam uploads ou downloads seguros e temporários sem expor credenciais.

#### **SNS (Simple Notification Service) e SQS (Simple Queue Service)**
*   **Definição:** SNS é um serviço de Pub/Sub para mensagens; SQS é um serviço de enfileiramento de mensagens.
*   **Como funciona:** O SNS distribui mensagens para múltiplos assinantes (fan-out); o SQS armazena mensagens em uma fila para serem processadas por um consumidor, desacoplando componentes.
*   **Caso de uso real:** Um sistema de pedidos envia uma notificação SNS que dispara simultaneamente um e-mail ao cliente e coloca uma mensagem em uma fila SQS para o sistema de estoque processar.
*   **Dicas para prova:** Lembre-se que as filas **SQS FIFO** garantem a ordem exata de processamento e entrega única.

#### **Amazon CloudWatch**
*   **Definição:** Serviço de monitoramento e observabilidade para recursos e aplicações na AWS.
*   **Como funciona:** Coleta métricas, armazena logs e permite definir alarmes que disparam ações automáticas.
*   **Caso de uso real:** Monitorar o uso de CPU de instâncias EC2 e disparar um alarme para iniciar novas instâncias quando necessário.
*   **Dicas para prova:** Use o **X-Ray** junto com CloudWatch para fazer tracing de requisições em microsserviços e identificar gargalos.

#### **Deployment (CI/CD na AWS)**
*   **Definição:** Conjunto de serviços para automatizar a entrega de software.
*   **Como funciona:** **CodePipeline** orquestra o fluxo; **CodeBuild** compila e testa; **CodeDeploy** implanta no destino.
*   **Caso de uso real:** Automatizar o provisionamento de infraestrutura RDS e EC2 em múltiplas contas de clientes usando **CloudFormation Stack Sets**.
*   **Dicas para prova:** Diferencie **CodeDeploy** (focado em implantação) de **CloudFormation** (focado em infraestrutura como código).

---

### 3. GLOSSÁRIO

*   **SDK (Software Development Kit):** Conjunto de bibliotecas para linguagens específicas (Java, .NET, Python) que simplifica a integração do código com os serviços AWS.
*   **CLI (Command Line Interface):** Ferramenta para gerenciar serviços AWS via linha de comando e automação por scripts.
*   **Serverless:** Modelo onde o provedor de nuvem gerencia a execução do código e a infraestrutura, cobrando apenas pelo uso real.
*   **Event-Driven Architecture:** Padrão onde ações no sistema são disparadas por mudanças de estado ou eventos específicos.
*   **IAM Role:** Identidade com permissões específicas que não possui credenciais de longo prazo, ideal para delegar acesso a serviços.
*   **IaC (Infrastructure as Code):** Prática de gerenciar infraestrutura através de arquivos de configuração (ex: CloudFormation, CDK) em vez de processos manuais.

---

### 4. QUESTÕES PRÁTICAS

1.  **Um desenvolvedor precisa distribuir atualizações de software globalmente com baixa latência e controle seguro de acesso. Qual a solução de menor custo?**
    *   A) Criar um bucket S3 em cada região.
    *   B) Usar Amazon CloudFront com URLs pré-assinadas para arquivos no S3.
    *   C) Usar AWS Lambda para replicar arquivos.
    *   D) Configurar instâncias EC2 com auto-scaling em cada continente.
    *   **Resposta correta:** **B**.
    *   **Explicação:** O CloudFront entrega conteúdo globalmente com baixa latência, e URLs pré-assinadas garantem acesso seguro e temporário sem custo de infraestrutura complexa.

2.  **Qual comando o desenvolvedor deve usar localmente para autorizar sua aplicação a interagir com a API da AWS usando permissões de um usuário IAM específico?**
    *   A) `aws login --username --password`
    *   B) `aws configure` para inserir Access Key e Secret Access Key.
    *   C) `aws sso connect`
    *   D) Instalar um certificado X.509 na máquina local.
    *   **Resposta correta:** **B**.
    *   **Explicação:** Para acesso programático fora do console, utilizam-se chaves de acesso (Access Key ID e Secret Access Key) configuradas via CLI ou SDK.

3.  **Uma função Lambda escrita em .NET Core interage apenas com DynamoDB e S3. Como minimizar o tempo de implantação e execução?**
    *   A) Aumentar o timeout da função para 15 minutos.
    *   B) Incluir todo o AWS SDK para .NET no pacote.
    *   C) Incluir apenas os módulos específicos do DynamoDB e S3 do SDK no pacote.
    *   D) Configurar a função para baixar o SDK do S3 durante o boot.
    *   **Resposta correta:** **C**.
    *   **Explicação:** Reduzir o tamanho do pacote de implantação incluindo apenas módulos necessários acelera o upload e a inicialização da função.

4.  **Uma aplicação de microsserviços apresenta problemas de latência intermitente. Qual ferramenta identificar o "caminho" da requisição e onde ocorre o atraso?**
    *   A) CloudWatch Logs.
    *   B) AWS CloudTrail.
    *   C) AWS X-Ray.
    *   D) Amazon Inspector.
    *   **Resposta correta:** **C**.
    *   **Explicação:** O X-Ray fornece mapas de serviço e visualizações de rastreamento (tracing) para analisar performance e erros em aplicações distribuídas.

5.  **Uma empresa precisa processar pedidos em ordem exata de chegada. Qual serviço garante esse requisito?**
    *   A) Filas Padrão do Amazon SQS.
    *   B) Amazon SNS.
    *   C) Filas FIFO do Amazon SQS.
    *   D) Amazon S3 com triggers.
    *   **Resposta correta:** **C**.
    *   **Explicação:** Diferente das filas padrão, as filas FIFO (First-In-First-Out) do SQS garantem a ordem de processamento e evitam mensagens duplicadas.

---

### 5. PROMPTS DE ESTUDO

*   **Explicação Simplificada:** "Aja como um instrutor AWS. Explique o conceito de AWS Lambda e como ele difere de uma instância EC2 usando uma analogia de cozinha."
*   **Comparação entre Serviços:** "Compare o Amazon SNS e o Amazon SQS. Em quais cenários eu deveria usar um em vez do outro para desacoplar minha aplicação?"
*   **Cenário Prático:** "Crie um roteiro passo a passo para configurar uma API serverless que salve dados no DynamoDB usando API Gateway e Lambda."

---

### 6. ERROS COMUNS

*   **Memorizar sem entender:** Tentar apenas decorar respostas de simulados é uma armadilha. A AWS foca no "porquê" por trás da arquitetura.
*   **Credenciais no código:** Nunca deixe Access Keys ou Secret Keys hardcoded. Use **IAM Roles** para serviços AWS e perfis de configuração localmente.
*   **Over-provisioning:** Importar o SDK completo quando apenas um módulo é necessário aumenta o custo e diminui a performance (especialmente em funções Lambda).
*   **Ignorar o Free Tier:** Muitos estudantes esquecem que podem praticar a maioria desses serviços (DynamoDB, S3, Lambda) sem custo dentro dos limites gratuitos da conta AWS.

---

### 7. RESUMO FINAL (REVISÃO RÁPIDA)

*   **IAM:** Sempre use **Roles** para permissões entre serviços.
*   **Lambda:** Configure **Simultaneidade Provisionada** para alta performance.
*   **S3:** Utilize **Presigned URLs** para uploads/downloads seguros.
*   **SQS:** Use filas **FIFO** se a ordem das mensagens for crítica.
*   **DynamoDB:** Lembre-se que é **NoSQL** e escalável com latência mínima.
*   **Observabilidade:** Use **X-Ray** para tracing e **CloudWatch** para métricas/logs.
*   **CI/CD:** CodePipeline orquestra, CodeBuild testa, CodeDeploy instala.
