# Guia de Estudo: AWS Certified Developer - Associate (DVA-C02)

Este material foi atualizado para incluir o seu Serverless Blueprint e representações visuais dos fluxos de arquitetura cobrados no exame.

--------------------------------------------------------------------------------
🚀 RECURSO COMPLEMENTAR
Para uma visualização detalhada de arquiteturas serverless, acesse o guia em PDF: 👉 AWS DVA-C02 Serverless Blueprint

--------------------------------------------------------------------------------
1. CONTEXTO E OBJETIVO
A certificação AWS Certified Developer - Associate (DVA-C02) valida a competência técnica em desenvolver, testar, implantar e depurar aplicações na nuvem AWS
. É recomendável que o candidato tenha um ou mais anos de experiência prática mantendo aplicações AWS
.
Distribuição de Tópicos (Domínios):
Desenvolvimento com Serviços AWS (32%): Foco em SDKs, integração de funções e bancos de dados
.
Segurança (26%): Autenticação, autorização e proteção de dados
.
Implantação (24%): CI/CD, gerenciamento de segredos e estratégias de lançamento
.
Solução de Problemas e Otimização (18%): Monitoramento, tracing e análise de performance
.

--------------------------------------------------------------------------------
2. RESUMO ESTRUTURADO DOS SERVIÇOS
IAM (Identity and Access Management)
Definição: Controla o acesso aos recursos da AWS com segurança
.
Como funciona: Permite criar identidades (usuários, grupos e funções) com permissões específicas definidas em arquivos JSON
.
Caso de uso real: Uma instância EC2 ou função Lambda assume uma IAM Role para ler arquivos de um bucket S3 sem precisar de chaves de acesso fixas no código
.
Dicas para prova: Nunca utilize credenciais de longo prazo (Access Keys) em produção; prefira IAM Roles
.
AWS Lambda
Definição: Computação serverless que executa código sem necessidade de gerenciar servidores
.
Como funciona: O código é disparado por eventos de outros serviços, escalando de zero a milhares de instâncias conforme a demanda
.
Caso de uso real: Redimensionar imagens automaticamente após o upload no S3
.
Dicas para prova: Para evitar a latência de inicialização (cold start), configure a Simultaneidade Provisionada
.
Amazon API Gateway
Definição: "Porta de entrada" para APIs que conecta aplicações front-end a serviços de back-end
.
Como funciona: Gerencia tráfego, autorização e controle de utilização (throttling)
.
Caso de uso real: Expor uma API REST para que um app mobile consulte dados no DynamoDB via Lambda
.
Dicas para prova: Entenda como o CORS funciona e como usar Autorizadores Lambda para segurança customizada
.
Amazon DynamoDB
Definição: Banco de dados NoSQL chave-valor escalável com performance consistente de milissegundos
.
Como funciona: Armazena dados em tabelas distribuídas por partições baseadas em uma Chave de Partição
.
Caso de uso real: Gerenciar o estado de sessões de usuários ou carrinhos de compras com alta carga de leitura/escrita
.
Dicas para prova: Use GSI (Índice Secundário Global) para consultas em atributos que não fazem parte da chave primária original
.
Amazon S3
Definição: Armazenamento de objetos de alta durabilidade e escalabilidade
.
Como funciona: Dados são armazenados como objetos em recipientes chamados Buckets
.
Caso de uso real: Hospedagem de sites estáticos ou armazenamento de logs de auditoria
.
Dicas para prova: Use URLs pré-assinadas para permitir uploads e downloads temporários e seguros
.
SNS (Simple Notification Service) e SQS (Simple Queue Service)
Definição: SNS é para notificações Pub/Sub; SQS é para enfileiramento de mensagens
.
Como funciona: O SNS envia a mesma mensagem para vários destinos (fan-out), enquanto o SQS armazena mensagens para processamento assíncrono, garantindo o desacoplamento
.
Caso de uso real: Um sistema de checkout que notifica o envio por e-mail (SNS) e coloca o pedido na fila de processamento (SQS)
.
Dicas para prova: Se a ordem das mensagens for crucial, use filas SQS FIFO
.
Amazon CloudWatch e AWS X-Ray
Definição: CloudWatch é para monitoramento de métricas/logs; X-Ray é para rastreamento (tracing) de requisições
.
Como funciona: O CloudWatch coleta dados operacionais em tempo real
; o X-Ray permite visualizar o caminho de uma requisição em microsserviços para encontrar gargalos
.
Caso de uso real: Disparar um alarme de CPU alta em instâncias EC2 ou rastrear por que uma função Lambda está lenta
.
Dicas para prova: X-Ray é a ferramenta correta para identificar latência em aplicações distribuídas
.
Deployment (CI/CD)
Definição: Automação da entrega de código
.
Como funciona: CodePipeline orquestra o fluxo; CodeBuild compila/testa; CodeDeploy implanta na infraestrutura
.
Caso de uso real: Atualizar automaticamente uma aplicação em contêineres ECS a cada commit no repositório
.
Dicas para prova: Saiba a diferença entre deploys Canary (gradual) e Blue/Green (troca completa)
.

--------------------------------------------------------------------------------
🖼️ DIAGRAMAS DE ARQUITETURA (VISUALIZAÇÃO)
Fluxo Serverless Padrão:
[Usuário] -> [API Gateway] -> [Lambda] -> [DynamoDB]
                |
          (Autorização via IAM ou Cognito)
Desacoplamento com SNS/SQS:
[Evento] -> [SNS Topic] --(Fan-out)--> [SQS Fila A] -> [Lambda 1]
                                 |---> [SQS Fila B] -> [Lambda 2]

--------------------------------------------------------------------------------
3. GLOSSÁRIO
SDK (Software Development Kit): Bibliotecas para integrar sua linguagem (Java, .NET, Python) com a AWS
.
Cold Start: Tempo de inicialização de uma função Lambda quando ela não é invocada há algum tempo
.
IaC (Infrastructure as Code): Uso de templates (CloudFormation/CDK) para criar infraestrutura
.
Payload: Os dados reais enviados em uma requisição de API ou mensagem de fila
.
Throttling: Limitação intencional de requisições para proteger o serviço de sobrecarga
.

--------------------------------------------------------------------------------
4. QUESTÕES PRÁTICAS
Qual a forma recomendada de fornecer permissões de acesso ao S3 para uma aplicação rodando em uma instância EC2?
Resposta: Criar uma IAM Role com as permissões necessárias e anexá-la à instância
.
Como garantir que as mensagens de uma fila sejam processadas exatamente na ordem em que foram enviadas?
Resposta: Utilizar o serviço Amazon SQS com o tipo de fila FIFO
.
Qual ferramenta ajuda um desenvolvedor a analisar o tempo gasto em cada componente de uma aplicação distribuída?
Resposta: AWS X-Ray
.
Para otimizar o tempo de inicialização de uma função Lambda que usa o AWS SDK, o que deve ser feito?
Resposta: Importar apenas os módulos específicos necessários do SDK em vez da biblioteca completa
.
Qual recurso do CloudWatch permite disparar uma ação automática quando uma métrica excede um limite?
Resposta: CloudWatch Alarms
.

--------------------------------------------------------------------------------
5. PROMPTS DE ESTUDO
"Compare SQS Standard vs FIFO. Explique as diferenças de throughput e garantias de entrega."
"Como configurar o CORS no API Gateway para permitir que um site estático no S3 consuma minha API?"
"Explique o fluxo de autenticação do Amazon Cognito User Pools para uma aplicação web."

--------------------------------------------------------------------------------
6. ERROS COMUNS
Decorar respostas: O banco de questões é enorme; foque em entender o "porquê" da arquitetura
.
Credenciais no código: Inserir chaves de acesso diretamente nos arquivos da aplicação é um risco grave de segurança
.
Não monitorar limites: Esquecer de configurar alarmes para custos ou limites de cota (Service Quotas)
.

--------------------------------------------------------------------------------
7. RESUMO FINAL (REVISÃO RÁPIDA)
Serverless: Lambda + API Gateway + DynamoDB
.
Segurança: Mínimo privilégio com IAM Roles
.
Mensageria: SQS para filas, SNS para notificações em massa
.
Observabilidade: Métricas no CloudWatch, rastreamento no X-Ray
.
SDK: Sempre inicialize clientes fora do handler da função Lambda para performance
.
