# AMI
## O que é uma AMI?
AMI (Amazon Machine Image) é uma imagem pré-configurada usada para criar instâncias EC2. Ela contém tudo o que a máquina precisa para inicializar e funcionar:
- Sistema operacional (Linux, Windows, etc.)
- Softwares e bibliotecas pré-instalados
- Configurações do sistema
- Dados e permissões opcionais

Ao lançar uma instância EC2, escolhemos uma AMI como base. Isso garante que todas as instâncias criadas a partir dela sejam idênticas em configuração e comportamento.

## Uso e benefícios das AMIs
1. Escalabilidade e automação: Permitem criar rapidamente várias instâncias idênticas — ideal para ambientes com auto scaling. Garantem consistência ao escalar aplicações sem precisar reconfigurar manualmente cada instância.

2. Backup e recuperação: Servem como ponto de restauração do estado atual de uma máquina. Caso algo dê errado em produção, podemos lançar uma nova instância a partir de uma AMI anterior.

3. Ambientes padronizados (Útil em pipelines CI/CD): as AMIs garantem que todos os ambientes (dev, staging, produção) usem a mesma base.

4. Redução de tempo de deploy: Ao incluir dependências e softwares na AMI, o tempo de inicialização de novas instâncias diminui significativamente.

# Snapshots EBS
## O que é um Snapshot EBS?
Um snapshot EBS é uma cópia de backup incremental e persistente de um volume EBS (Elastic Block Store). Ele captura o estado dos dados armazenados em um volume EBS em um determinado momento. Os snapshots são armazenados no Amazon S3 (de forma gerenciada pela AWS), mas acessamos e gerenciamos diretamente pelo serviço EBS.

Eles são fundamentais para backup, recuperação de desastres, migração e criação de novos volumes na AWS.

## Uso e benefícios dos Snapshots EBS
1. Backup e recuperação de dados:  Snapshots servem como backup confiável dos volumes EBS. Podemos restaurar o volume ao estado exato do momento do snapshot.

2. Criação de novos volumes: Snapshots podem ser usados para criar novos volumes EBS idênticos ao original. Isso facilita escalar sistemas ou criar ambientes de teste a partir de dados reais.

3. Migração entre regiões e contas: Snapshots podem ser copiados entre regiões ou contas da AWS, facilitando disaster recovery ou expansão global.

4. Base para AMIs:  AMIs utilizam snapshots dos volumes raiz para armazenar o sistema operacional e dados. Por isso, snapshots são parte essencial do processo de criação de AMIs.

## Características importantes
- Incrementais: somente as alterações desde o último snapshot são armazenadas, economizando espaço e reduzindo custos.
- Ponto no tempo: capturam o estado do volume em um momento específico.
- Armazenamento durável: ficam salvos no S3 de forma segura e redundante.
- Consistência: para dados críticos (como bancos de dados), é recomendado parar a gravação no volume ou congelar o sistema de arquivos antes de criar o snapshot.

## Custos
- Pagamos pelo armazenamento dos dados do snapshot (em GB/mês).
- Como são incrementais, snapshots subsequentes custam menos do que backups completos.
- Cópias entre regiões têm custos adicionais de transferência de dados.

# EC2
## O que é o Amazon EC2?
Amazon EC2 (Elastic Compute Cloud) é um dos serviços principais da AWS que permite criar e executar máquinas virtuais na nuvem, chamadas de instâncias.
Ele fornece capacidade de computação elástica, escalável e sob demanda, usada para hospedar aplicações web, APIs, bancos de dados, sistemas de processamento, microsserviços, e muito mais.

## Recursos e Benefícios
1. Elasticidade e Escalabilidade: Escalar verticalmente conforme a demanda (manualmente ou via Auto Scaling Groups). Permite criar várias instâncias idênticas rapidamente.

2. Diversidade de tipos e tamanhos: Instâncias otimizadas para computação, memória, armazenamento ou GPU.

3. Modelos de compra flexíveis: 
   - On-Demand: paga por hora/segundo de uso.
   - Reserved Instances: mais baratas, exigem compromisso de 1 ou 3 anos.
   - Spot Instances: extremamente baratas, mas podem ser interrompidas.
   - Savings Plans: modelo flexível com desconto baseado em uso previsto.

4. Integração com outros serviços:  EC2 funciona em conjunto com S3, EBS, CloudWatch, Lambda, IAM, etc., formando infraestruturas completas.

## Custos
Baseados no tipo de instância, região, tempo de uso e armazenamento. Pagamos separadamente por instância (CPU/RAM), armazenamento EBS e tráfego de rede (saída).
Dica: Usar a calculadora de custos da AWS para planejar e prever gastos.

## Exemplo de arquitetura usando EC2
![Diagrama usando EBS e EC2](https://github.com/jesslourenco/aws-dio-projects/blob/main/images/diagrama-ec2.png)
- O usuário (Actor) envia um arquivo pela aplicação.
- O arquivo é armazenado inicialmente no volume D - EBS.
- A instância EC2 acessa esse volume, processa o arquivo e realiza operações necessárias.
- Durante o processamento, a EC2 pode ler ou gravar informações no RDS.
- Após o processamento, os resultados são gravados no volume E - EBS.
