# O que é o LocalStack?

LocalStack é uma plataforma que emula serviços da AWS localmente no seu ambiente de desenvolvimento, permitindo que você desenvolva, teste e valide aplicações que usam serviços da AWS sem precisar de uma conta real nem gerar custos na nuvem.

Ele roda em um container Docker e simula diversos serviços populares, como S3, Lambda, DynamoDB, API Gateway, SQS, SNS, CloudWatch, entre outros. Isso o torna extremamente útil para testes automatizados, desenvolvimento offline e ambientes de CI/CD.

Em outras palavras, o LocalStack funciona como uma “mini AWS” rodando no seu computador, o que acelera muito o ciclo de desenvolvimento.

# Principais funcionalidades e benefícios
- Emulação local de mais de 60 serviços da AWS.
- Desenvolvimento e testes sem custos, sem risco de alterar recursos reais em produção.
- Ciclo de desenvolvimento mais rápido, sem necessidade de implantar código na nuvem a cada alteração.
- Integração com ferramentas oficiais da AWS, como o AWS CLI, SDKs e Terraform.
- Ideal para pipelines de CI/CD, permitindo testes automatizados consistentes.

# Caso de uso: Sistema de Processamento de Notas Fiscais
![Caso de uso](https://github.com/jesslourenco/aws-dio-projects/blob/main/desafio-tarefas-automatizadas/images/case.png)
# Fluxo do sistema e Localstack
Com o LocalStack, podemos simular todo o fluxo do projeto localmente, seguindo o processo real que aconteceria na AWS:
1. Upload de arquivo no S3 – O usuário envia um arquivo (por exemplo, CSV ou JSON) para um bucket S3 simulado pelo LocalStack.
2. Disparo automático da Lambda – O evento de upload no S3 aciona uma função Lambda escrita em Python.
3. Processamento do arquivo – A função Lambda lê e processa o conteúdo do arquivo (por exemplo, extrai dados ou formata informações) e grava os resultados em uma tabela no DynamoDB.
4. Consulta via API – Uma segunda função Lambda consulta os dados gravados no DynamoDB e os expõe por meio de uma API Gateway local, permitindo que outros sistemas ou aplicações consumam essas informações.
