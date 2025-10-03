# O que é o AWS CloudFormation?
AWS CloudFormation é um serviço que permite criar, provisionar e gerenciar recursos da AWS de forma automática e declarativa usando arquivos de configuração (em YAML ou JSON). Em vez de criar recursos manualmente pelo console, você descreve toda a infraestrutura, redes, instâncias, bancos de dados, permissões, funções Lambda e muito mais — em um template, e o CloudFormation cuida de criar, atualizar e excluir tudo na ordem certa e de forma segura. Ou seja: IaC :)

# Principais funcionalidades 
- Infraestrutura como Código (IaC): descreva todos os seus recursos AWS em um arquivo legível e versionável.
- Stacks: conjuntos de recursos criados, atualizados ou excluídos juntos com base no template.
- StackSets: permitem implantar stacks em várias contas e regiões ao mesmo tempo.
- Automação de dependências: o CloudFormation entende a relação entre os recursos e cria tudo na ordem correta.
- Rollback automático: se algo falhar na criação ou atualização, ele reverte para o estado anterior automaticamente.
- Suporte a parâmetros e variáveis: permite tornar os templates dinâmicos e reutilizáveis.
- Saídas (Outputs): exporta informações importantes dos recursos criados (ex.: endpoint de API, nome de bucket etc.).
- Integração com CI/CD: pode ser facilmente integrado em pipelines de automação (CodePipeline, GitHub Actions, etc.).

# Benefícios
- Automação e consistência: evita erros humanos e garante ambientes idênticos em dev, staging e produção.
- Escalabilidade: cria centenas de recursos com um único comando.
- Controle de versão: como os templates são arquivos de texto, você pode versioná-los no Git.
- Facilidade de replicação: implante a mesma infraestrutura em diferentes contas e regiões de forma rápida.
- Segurança e governança: facilita auditoria e documentação da infraestrutura.
- Menor tempo de provisionamento: elimina a necessidade de cliques manuais no console.

# Estrutura básica de um template
AWSTemplateFormatVersion: "2010-09-09"
Description: "Exemplo simples de CloudFormation - criação de uma instância EC2"

Resources:
  MyEC2Instance:
    Type: "AWS::EC2::Instance"
    Properties:
      InstanceType: t2.micro
      ImageId: ami-0abcdef1234567890