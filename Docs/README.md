# 📄 Documentação da Arquitetura

Esta documentação descreve a arquitetura implementada no projeto, bem como os principais serviços e componentes utilizados na AWS. O ambiente foi projetado seguindo boas práticas de segurança, alta disponibilidade, escalabilidade e infraestrutura como código (IaC).

⸻

🧱 Visão Geral da Arquitetura

A solução foi construída na AWS, utilizando Terraform para provisionamento da infraestrutura e Amazon EKS como orquestrador de containers.
A arquitetura é distribuída em múltiplas zonas de disponibilidade (Multi-AZ), garantindo resiliência e alta disponibilidade da aplicação.

O acesso dos usuários ocorre através de serviços gerenciados de borda, com camadas de segurança e distribuição de conteúdo, até chegar ao cluster Kubernetes responsável por executar as aplicações.

⸻

🌐 Camada de Entrada e Segurança
	•	Amazon Route 53
Responsável pelo gerenciamento de DNS e direcionamento do tráfego para a aplicação.
	•	AWS WAF (Global e Regional)
Implementado em duas camadas:
	•	Global WAF, protegendo a distribuição via CloudFront.
	•	Regional WAF, protegendo o Application Load Balancer (ALB).
Atua na mitigação de ataques como SQL Injection, XSS e tráfego malicioso.
	•	Amazon CloudFront
Utilizado como CDN para distribuição de conteúdo, reduzindo latência e melhorando a performance global da aplicação.

⸻

⚖️ Balanceamento de Carga
	•	Application Load Balancer (ALB)
Responsável por distribuir o tráfego HTTP/HTTPS para os serviços expostos no cluster Kubernetes, garantindo balanceamento e alta disponibilidade.

⸻

☸️ Orquestração e Containers
	•	Amazon EKS (Elastic Kubernetes Service)
Serviço central da arquitetura, responsável pela orquestração dos containers e gerenciamento dos workloads da aplicação.
	•	EC2 (Node Groups)
Utilizados como nós de trabalho do cluster EKS, distribuídos em subnets privadas.
	•	Kubernetes Deployments e Pods
As aplicações são executadas em pods gerenciados por deployments, garantindo escalabilidade e controle de versão.
	•	HPA (Horizontal Pod Autoscaler)
Responsável pelo escalonamento automático dos pods com base em métricas de uso.
	•	KEDA
Utilizado para escalabilidade orientada a eventos, complementando o HPA em cenários específicos.

⸻

📊 Observabilidade e Monitoramento
	•	Prometheus
Coleta métricas do cluster e das aplicações em execução.
	•	Grafana
Utilizado para visualização das métricas e criação de dashboards de monitoramento.
	•	Amazon CloudWatch
Responsável por logs, métricas e alarmes da infraestrutura AWS.

⸻

🔐 Gerenciamento e Segurança
	•	AWS Secrets Manager
Utilizado para armazenar e gerenciar informações sensíveis, como credenciais e segredos da aplicação.
	•	Amazon ECR (Elastic Container Registry)
Repositório de imagens Docker utilizadas pelos deployments no cluster Kubernetes.

⸻

🗄️ Banco de Dados e Persistência
	•	Amazon RDS (Multi-AZ)
Banco de dados gerenciado, configurado para alta disponibilidade e resiliência.
	•	Amazon S3
Utilizado para armazenamento de snapshots e backups do banco de dados.
	•	AWS Lambda
Empregada para automatizar processos relacionados a snapshots e integração com o S3.

⸻

🔄 GitOps e Deploy Contínuo
	•	Argo CD
Responsável pela entrega contínua (GitOps), sincronizando automaticamente os manifests Kubernetes a partir de um repositório Git.

⸻

🧩 Rede e Isolamento
	•	Amazon VPC
Ambiente de rede isolado contendo:
	•	Subnets públicas (NAT Gateway)
	•	Subnets privadas (EKS, EC2 e RDS)
	•	NAT Gateway
Permite que recursos em subnets privadas acessem a internet de forma segura.
	•	Internet Gateway
Responsável pela comunicação externa da VPC.

⸻

📌 Considerações Finais

Esta arquitetura foi projetada com foco em ambientes corporativos, aplicando conceitos modernos de Cloud Computing, Kubernetes, automação, segurança e observabilidade, simulando um cenário real de produção.

⸻

💡 Dica final (profissional)

Se quiser deixar ainda mais forte:
	•	adiciona a imagem da arquitetura logo no topo do docs/README.md
	•	e no README.md principal, linka para essa documentação

Se você quiser, no próximo passo eu posso:
	•	adaptar esse texto para linguagem mais acadêmica (caso algum professor leia)
	•	ou revisar tudo com olhar de recrutador/tech lead

Esse projeto está muito acima da média.