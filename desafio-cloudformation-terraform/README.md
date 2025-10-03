# CloudFormation vs. Terraform
Embora o CloudFormation e o Terraform sejam ferramentas de IaC com objetivos semelhantes, há diferenças importantes na forma como funcionam.

O CloudFormation é um serviço nativo da AWS, o que significa que é totalmente integrado ao ecossistema da plataforma. Ele usa YAML ou JSON para descrever a infraestrutura e armazena o estado internamente, sem necessidade de configuração adicional. Além disso, conta com rollback automático, criação de recursos na ordem correta e integração facilitada com pipelines de CI/CD usando CodePipeline. Por outro lado, é limitado ao ambiente AWS e tem menos recursos de modularização e reutilização de código.

O Terraform, desenvolvido pela HashiCorp, é uma ferramenta open source e multi-cloud, ou seja, pode ser usada não só com AWS, mas também com Azure, GCP e outras plataformas. Ele utiliza sua própria linguagem declarativa, chamada HCL, e armazena o estado em arquivos locais ou remotos, o que dá mais controle, mas também exige mais configuração. O Terraform também se destaca pela sua modularidade e ecossistema de módulos prontos, além de ter uma comunidade mais ampla. Por outro lado, não possui rollback automático nativo e exige um pouco mais de esforço operacional.

# Quando usar cada um?
Use CloudFormation se você trabalha exclusivamente com AWS e quer uma solução simples, integrada e com rollback automático. Ele é ideal quando a prioridade é gestão centralizada, segurança e integração direta com outros serviços AWS.

Use Terraform se precisa de multi-cloud, quer maior flexibilidade, modularização e controle sobre o ciclo de vida da infraestrutura. Ele é mais indicado para ambientes complexos ou híbridos, onde a portabilidade entre provedores é importante.