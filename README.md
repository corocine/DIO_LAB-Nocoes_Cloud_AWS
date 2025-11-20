# Projeto de Infraestrutura Cloud - Abstergo Industries


## Visão Geral do Projeto

Este documento detalha o plano de implementação de infraestrutura em nuvem para a **Abstergo Industries**. O objetivo de negócio é transformar a operação farmacêutica em uma **revendedora B2B** para outras farmácias.

Como a empresa não possuía infraestrutura prévia (cenário *Greenfield*), a arquitetura foi desenhada com foco total em **Redução de Custos** e elasticidade. A estratégia adotada foi **Serverless**, garantindo que a empresa pague apenas pelo uso real, sem custos de servidores ociosos.

---

## Serviços AWS Selecionados

A arquitetura foi dividida em três camadas estratégicas para maximizar a eficiência financeira:

### 1. Front-end e Content Delivery
**Serviços:** `Amazon S3` + `Amazon CloudFront`

* **Foco:** Hospedagem estática e CDN global.
* **Caso de Uso:** Hospedagem do portal de revenda (SPA - Single Page Application).
* **Justificativa de Custo:** Elimina a necessidade de servidores web rodando 24/7. O custo é baseado apenas em armazenamento e transferência de dados (GB transferido). Se não houver acessos, o custo é virtualmente zero. Amazon S3, para os arquivos o site e CloudFront para CDN.

### 2. Back-end e Regras de Negócio
**Serviço:** `AWS Lambda`

* **Foco:** Computação *Serverless*.
* **Caso de Uso:** Processamento de pedidos, cálculo de impostos e validação de estoque.
* **Justificativa de Custo:** Cobrança por milissegundos de execução. Aproveitamento do *Free Tier* da AWS (1 milhão de requisições mensais gratuitas), ideal para o início da operação.

### 3. Banco de Dados
**Serviço:** `Amazon DynamoDB`

* **Foco:** Banco de dados NoSQL Serverless de ultra performance.
* **Caso de Uso:** Armazenamento do catálogo de medicamentos, gestão de estoque em tempo real e status dos pedidos (Carrinho de Compras).
* **Justificativa de Custo:** Elimina o custo de "instância ligada". O modelo de cobrança é sob demanda (*on-demand*): a empresa paga apenas por leitura e gravação realizada. Se houver 0 pedidos na madrugada, o custo do banco de dados nesse período é $0.

# Conclusão

Como a implementação da infraestrutura cloud para a **Abstergo Industries** parte de um cenário do zero, a arquitetura foi desenhada com foco estratégico em **eficiência de custos** e elasticidade. A escolha pelo modelo **Serverless** permite acompanhar a evolução do negócio, mantendo os custos iniciais baixos e escalando recursos automaticamente apenas quando necessário.
