# fullcycle-imersao13

Treinamento com as aulas gratuitas da imersão no Youtube

<br/><br/>

# Tecnologias

- Docker
- Linguagem Go
- Next.js
- Nest.js
- Apache Kafka
- SSE (Server Sent Events)

![Tecnologias Abordadas nas Aulas do Curso](docs/images/tecnologias_abordadas_nas_aulas_do_curso.png)

<br/><br/>

# Agenda

- Entender o projeto prático
- Tecnologias que serão utilizadas
- Ordem do desenvolvimento
- Entendimento do microsserviço de "bolsa"
- Inicio do microsserviço de "bolsa"

<br/><br/>

# Projeto prático

**Desenvolveremos uma plataforma de investimentos com Home Broker:**

- Sistema da Bolsa (Simular uma B3 - Dar Match de ofertas de compra e vendas de ações)
- Home Broker onde as ofertas serão submetidas, além dos indicadores em tempo real

![Dinamica do projeto](docs/images/dinamica_do_projeto.png)

<br/><br/>

# Ordem do desenvolvimento

- Dia 1: Criação do microsserviço de bolsa com seu principal algoritmo funcionando.
- Dia 2: Adoção do Apache Kafka ao microsserviço de bolsa para enviar e receber as ordens
- Dia 3: Desenvolvimento do backend (Nest.js) do Home Broker
- Dia 4: Desenvolvimento do frontend (Next.js) do Home Broker
- Dia 5: Integração do Frontend e Backend e ajustes finos

<br/><br/>

# Recomendações

- Assista as lives do "esquenta"
  - Falamos sobre: Docker, Go, Kafka, Nest.js e Next.js
  - Encontram-se no canal do YouTube: YouTube.com/fullcycle

<br/><br/>

# Complexidades do microsserviço de "Bolsa"

- Simulador da bolsa possui um algoritmo ligeiramente complexo para fazer o match das ordens de compra e venda
- Simulador precisa ser performático
- Precisará trabalhar com as operações "in memory"
- Principais alocações precisarão ficar na heap e não na stack

![Filas Ordem de Compra e Ordem de Venda](docs/images/filas_ordem_de_compra_e_ordem_de_venda.png)

<br/><br/>

# Microsserviço de "Bolsa"

- Cada vez que uma ordem de compra e venda dão “match”, geraremos uma transação.
- Essa transação será publicada no Apache Kafka no formato JSON
- Não utilizaremos banco de dados por conta de tempo e simplificação
- Sim, se o processo morrer, perderemos transações (lembrando estamos simplificando)

<br/><br/>

# Microsserviço de "Bolsa" - Channels

- Quando um "match" ocorre, uma "transaction" é gerada e enviada a um channel de output que será lido pelo Apache Kafka

```mermaid
flowchart LR;
  A["
Book.trade
(async)"]-->B[Transaction channel]-->C[Apache Kafka];
```
