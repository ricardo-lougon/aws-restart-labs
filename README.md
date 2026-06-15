# AWS re/Start - Laboratórios Práticos

Bem-vindo ao repositório de laboratórios práticos realizados durante o programa **AWS re/Start**. Este repositório contém documentações e evidências técnicas de configurações em ambiente AWS, abrangendo desde fundamentos de computação até automação e machine learning.

## 📁 Estrutura do Repositório

Os laboratórios estão organizados por módulos temáticos para facilitar a consulta:

### 1. EC2, IAM e Armazenamento

* **EC2** — *Amazon EC2: Provisionamento de Infraestrutura via Console e AWS CLI — Host Bastion e Servidor Web.* Host bastion provisionado pelo Console como ponto de execução da automação via CLI; servidor web criado integralmente por linha de comando, com Apache e aplicação instalados automaticamente via User Data.
* **Desafio EC2** — *Amazon EC2 — Challenge Lab: Construção de Infraestrutura Completa do Zero — VPC, Sub-rede Pública, Servidor Web e Implantação de Aplicação.* VPC, sub-rede pública, internet gateway e tabela de rotas criados do zero; instância EC2 provisionada na rede com Apache instalado automaticamente via User Data.
* **Troubleshooting** — *Amazon EC2 — Troubleshooting: Diagnóstico e Correção de Dois Bugs Reais em Script CLI de Implantação de Pilha LAMP.* Dois bugs diagnosticados e corrigidos em script de implantação LAMP; execução de ponta a ponta validada pelo cloud-init e pela aplicação da cafeteria (menu, pedidos, histórico).
* **IAM** — *AWS IAM — Introdução ao Identity and Access Management: Controle de Acesso por Função com o Princípio do Menor Privilégio.* Modelo de controle de acesso por grupos IAM, política de senhas configurada para a conta, três usuários atribuídos a grupos, com seis cenários de teste validando permissões e negações.
* **AWS CLI** — *AWS CLI — Instalação em Red Hat Linux, Configuração de Credenciais e Consulta Programática ao AWS IAM.* AWS CLI v2 instalada em Red Hat Linux, autenticação por chaves de acesso validada com `aws iam list-users`, e política IAM recuperada sem Console via `list-policies` + `get-policy-version`.
* **EBS** — *Amazon EBS — Ciclo de Vida Completo de Volume: Criação, Formatação, Montagem, Snapshot e Restauração de Dados.* Volume criado, formatado em ext3, montado com `/etc/fstab`, snapshot criado, dados simuladamente perdidos e restaurados a partir do snapshot em novo volume.
* **Armazenamento** — *Gerenciamento de Armazenamento AWS — Automação de Snapshots EBS com cron e Python + Sincronização S3 com Política de Retenção e Recuperação por Versionamento.* Snapshots EBS automatizados via cron com política de retenção em Python (`snapshotter_v2.py`); sincronização S3 versionada com recuperação de exclusão acidental via `list-object-versions` + `get-object`.

### 2. S3

* **Site Estático** — *Amazon S3 — Site Estático: Publicação de Site Estático via AWS CLI com IAM, Session Manager e Script de Deploy Incremental.* Bucket, permissões, usuário IAM, upload e hospedagem estática configurados via CLI; acesso à instância via Session Manager sem porta SSH aberta.
* **Desafio S3** — *Amazon S3 — Challenge Lab: Fundamentos Operacionais do S3 em Formato Open-Ended — Bucket, Objeto, Permissões e Inspeção via CLI.* Bucket e objeto criados, comportamento padrão de acesso negado confirmado, e objeto específico tornado público via permissões em camadas, sem expor o bucket inteiro.
* **S3 Avançado** — *Amazon S3 — Avançado: Compartilhamento Seguro entre Organizações com IAM Granular por Prefixo, Auditoria Bidirecional de Permissões e Notificações de Eventos via SNS.* Política IAM com três statements restringindo usuário a prefixo `images/`, validada em cinco cenários de auditoria; pipeline S3 → SNS → e-mail validado para upload e exclusão de objetos.

### 3. Banco de Dados e Rede

* **RDS** — *Amazon RDS — Banco de Dados MySQL Gerenciado com Alta Disponibilidade Multi-AZ: Infraestrutura, Segurança de Rede e Integração com Aplicação Web.* DB Security Group e DB Subnet Group provisionados; instância MySQL Multi-AZ com standby em AZ distinta; aplicação Address Book conectada via endpoint RDS com CRUD validado.
* **Migração** — *Migração para Amazon RDS — Lift & Shift de Banco Local (EC2/MariaDB) para Amazon RDS: Infraestrutura via CLI, Migração com mysqldump, Reconfiguração via SSM e Monitoramento com CloudWatch.* Infraestrutura RDS provisionada via CLI; banco `cafe_db` migrado com `mysqldump` e validado por contagem de registros; aplicação reconfigurada apenas via parâmetro `/cafe/dbUrl` no SSM, sem alteração de código.
* **VPC** — *Amazon VPC — Construção de Rede Virtual Completa do Zero: Sub-redes, Internet Gateway, NAT Gateway, Tabelas de Rota e Bastion Host.* VPC com CIDR 10.0.0.0/16 e DNS habilitado; sub-redes pública/privada dimensionadas; IGW e NAT Gateway configurados; Bastion Host validado como ponto de acesso à sub-rede privada.
* **VPC Troubleshooting** — *Troubleshooting de VPC — Diagnóstico e Correção de Dois Problemas de Rede via AWS CLI: Tabela de Rotas, ACL de Rede, VPC Flow Logs e Análise com grep.* Diagnóstico em camadas via CLI: rota `0.0.0.0/0` ausente (camada 4) e regra DENY na ACL (camada 5) corrigidas; VPC Flow Logs analisados com `grep` confirmaram cada tentativa bloqueada.

### 4. Computação Avançada

* **Systems Manager** — *AWS Systems Manager — Gerenciamento de Infraestrutura sem SSH: Inventário, Run Command, Parameter Store e Session Manager.* Inventory, Run Command (instalação de app sem SSH), Parameter Store (feature toggle em tempo real) e Session Manager (terminal via navegador sem porta 22) validados.
* **ELB + Auto Scaling** — *ELB + EC2 Auto Scaling — Evolução de Instância Única para Alta Disponibilidade Multi-AZ com Application Load Balancer, Auto Scaling e Monitoramento CloudWatch.* ALB em duas AZs com health check; Auto Scaling Group provisionando instâncias saudáveis; teste de carga disparou alarme CloudWatch e scale-out automático.
* **Auto Scaling CLI** — *Auto Scaling via CLI + Console: Criação de AMI com Hardening de Segurança via AWS CLI + Orquestração de ALB e Auto Scaling pelo Console — Abordagem Híbrida de Pipeline.* Instância criada via CLI com hardening de segurança e captura de AMI; ALB e ASG orquestrados pelo Console; teste de estresse acionou scale-out de 2 para 3 instâncias.
* **Route 53** — *Amazon Route 53 — DNS como Componente Ativo de Resiliência: Failover Multi-AZ com Health Check, Notificações SNS e RTO Quantificado em Menos de 35 Segundos.* Health check com intervalo de 10s detectou falha em 20s; failover DNS confirmado pela mudança de AZ exibida no site; RTO total inferior a 35 segundos.

### 5. Serverless e Notificações

* **Lambda** — *AWS Lambda — Serverless: Pipeline de Relatório Diário Orientado a Eventos — EventBridge, Duas Funções Lambda em Cadeia, MySQL via VPC, SSM Parameter Store e Entrega via SNS.* Camada `pymysqlLibrary` associada à função `DataExtractor`; timeout de conexão ao banco corrigido via security group; função `salesAnalysisReport` deployada via CLI, entregando relatório diário por e-mail via EventBridge → Lambda → MySQL → SNS.
* **Desafio Lambda** — *AWS Lambda — Challenge Lab: Contador de Palavras Serverless com Gatilho S3, Lambda Python e Notificação SNS — Solução Open-Ended sem Roteiro.* Pipeline construído em autonomia total, sem roteiro: upload → evento S3 → Lambda (código Python escrito do zero) → SNS → e-mail, com contagens e formato de mensagem validados em três arquivos de teste.

### 6. Monitoramento, Governança e Segurança

* **CloudWatch** — *Infraestrutura de Monitoramento — Observabilidade Completa em Quatro Camadas: CloudWatch Agent, Logs e Filtros de Métrica, Alarmes SNS, Events e AWS Config.* CloudWatch Agent instalado via SSM Run Command e configurado pelo Parameter Store; filtro de métrica sobre erros 404 disparando alarme e e-mail SNS; CloudWatch Events detectando parada de instância em tempo real.
* **CloudTrail** — *AWS CloudTrail — Investigação Forense de Incidente de Segurança: Trilha, Análise com grep/CLI/Athena, Identificação do Invasor e Remediação Completa.* Usuário IAM malicioso identificado via evento `AuthorizeSecurityGroupIngress` nos logs Athena (nome, IP, horário); remediação em cinco vetores — sessão encerrada, usuário removido, SSH por senha desativado, regra `0.0.0.0/0` excluída, imagem restaurada a partir de backup.
* **Tags** — *Gerenciamento de Recursos com Tags — Consultas JMESPath, Atualização em Lote, Automação FinOps com Stopinator e Política Tag-or-Terminate via PHP SDK.* Consultas JMESPath tabulares com extração de tags aninhadas; atualização em lote da tag `Version` restrita a instâncias específicas; "stopinator" reiniciando instâncias em todas as regiões; política tag-or-terminate encerrando instâncias sem tag `Environment`.

### 7. Otimização e IaC

* **Otimização** — *Otimização de Infraestrutura — Rightsizing EC2, Remoção de Serviços Ociosos e Quantificação de Economia com AWS Pricing Calculator: Ciclo Completo de FinOps.* MariaDB local removido após migração para RDS; instância redimensionada de `t3.small` para `t3.micro` via `stop → modify → start`; economia de US$ 10,42/mês (29%) quantificada na Pricing Calculator.
* **CloudFormation** — *AWS CloudFormation — Infraestrutura como Código: Template YAML Evolutivo com VPC, S3, EC2, AMI Dinâmica via SSM e Ciclo de Vida Completo de Pilha.* Pilha criada com 5 recursos de rede, expandida autonomamente com bucket S3 e instância EC2 (AMI dinâmica via SSM), e excluída por completo; Change Sets confirmaram alterações isoladas em cada atualização.
* **CFN Troubleshooting** — *CloudFormation — Troubleshooting: Diagnóstico de WaitCondition com DO_NOTHING, Detecção de Configuration Drift e Exclusão Parcial de Pilha com retain-resources.* Typo `http`→`httpd` identificado via `--on-failure DO_NOTHING` e log do cloud-init; drift do security group detectado via `detect-stack-drift`; exclusão parcial de pilha com `--retain-resources` preservando bucket S3.
* **Desafio CFN** — *CloudFormation Challenge Lab — Template YAML Criado do Zero: VPC, Internet Gateway, Grupo de Segurança, Sub-rede e Instância EC2 com Autonomia Total e Iteração Documentada.* Template com seis recursos criado do zero e provisionado em `CREATE_COMPLETE`, seguindo o grafo de dependências (VPC → IGW/Attachment → SG/Sub-rede → EC2); validação via Console e CLI com JMESPath.

### 8. Machine Learning

* **SageMaker** — *Amazon SageMaker — ML: Treinamento de Modelo de Classificação Biomecânica com XGBoost — Data Split, Hiperparâmetros e Pipeline MLOps no Amazon SageMaker.* Dados biomecânicos divididos em 70/20/10 com reprodutibilidade, formatados para o SageMaker e enviados ao S3; Estimator XGBoost treinado em `ml.m5.xlarge`; artefato `model.tar.gz` salvo automaticamente no S3.

---
*Repositório mantido por Ricardo Neves Lougon.*
