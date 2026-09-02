# Fabrício Júnio

*[Read this in English](README.en.md)*

Desenvolvedor back-end em Bauru/SP. Java e Spring Boot, integração e sistemas que conversam por
evento. No trabalho, processos que já estão rodando em empresa grande, com instâncias em
andamento no momento em que a alteração sobe.

[LinkedIn](https://linkedin.com/in/fabríciojúnio) · [Portfólio](https://portfolio-a3qn.vercel.app) · junioad555@gmail.com

## O que eu faço

Sou desenvolvedor na área de Serviços da Digihub Tecnologia, do grupo Lecom, atendendo treze
clientes de seguros, saúde, cooperativismo de crédito, auditoria e judiciário. O dia é receber
um chamado, entender o processo, medir o que acontece em produção, propor, desenvolver,
homologar e publicar. Na prática: integração e robô em Java, regra de tela em JavaScript,
roteamento de processo, SQL de diagnóstico e automação RPA.

O hábito que trouxe daí para todo código que escrevo: eu meço antes de mexer. Reproduzo a regra
atual, rodo contra o histórico real e só confio no modelo quando ele acerta o passado. Se a
simulação não prevê o que já aconteceu, não serve para prever o que vai acontecer.

**Stack:** Java 21 · Spring Boot · Kafka · SQL · PostgreSQL · Docker · Kubernetes · AWS
**Também uso:** Node/NestJS · TypeScript · Next.js · Python

## Projetos

### [Feira do Comando](https://github.com/fabriciojunio/feira-do-comando)
`Java 21 · Spring Boot · Kafka · PostgreSQL · MongoDB · Terraform · Kubernetes`

Pedidos orientados a eventos. Quatro serviços com banco próprio, nenhum lendo tabela do outro.
A saga precisa sobreviver a mensagem repetida, fora de ordem e atrasada, e o caso que mais deu
trabalho foi a corrida em que o pagamento é aprovado durante o cancelamento. Outbox transacional
com `SELECT FOR UPDATE SKIP LOCKED`, para rodar em várias instâncias, e consumidor idempotente
pelo inbox. Concorrência provada com dez threads reais contra um PostgreSQL real, não com
simulação: 108 pedidos por segundo, impressos na saída do build. A infraestrutura está em
Terraform, com VPC de sub-rede privada, RDS, ECR e Kafka gerenciado.

### [Vitrine Bauru](https://github.com/fabriciojunio/vitrine-bauru)
`Java 21 · Spring Boot · Kafka · Amazon SNS e SQS · PostgreSQL · React 19`

No ar, em parceria com a Secretaria de Desenvolvimento Econômico de Bauru. O transporte de
eventos é uma interface com três adaptadores: Kafka onde existe corretor, Amazon SNS na
implantação gerenciada, e entrega dentro do próprio processo quando não há corretor nenhum.
Trocar o transporte muda a rede sem mexer nas garantias. A exclusão de dados pela LGPD é uma
saga com prazo e reenvio, em que três serviços precisam confirmar antes de o pedido fechar.
1.042 testes que sobem PostgreSQL e Kafka embarcados, sem exigir Docker instalado.
[No ar](https://vitrine-bauru.vercel.app)

### [Outorga](https://github.com/fabriciojunio/outorga)
`Java · Spring Boot · Next.js · PostgreSQL`

Streaming white-label multi-tenant em que a licença de exibição é invariante de domínio: não
existe caminho de código que publique conteúdo sem ela. A regra não fica num `if` do
controlador, fica no lugar onde não dá para desviar.

### [CodeReview AI](https://github.com/fabriciojunio/codereview-ai)
`Java 21 · Spring Boot · RabbitMQ · Redis · PostgreSQL · Ollama`

Análise de código com modelo de linguagem rodando local, então o código não sai da rede. A
submissão devolve um ticket e cai numa fila, o resultado volta por Server-Sent Events conforme o
modelo gera, e o Redis guarda 24h pelo hash do código. 88 testes, os de integração com
Testcontainers.

### [ConectAgente](https://github.com/fabriciojunio/ConectAgente)
`React Native · Expo · SQLite · Supabase`

App para Agente Comunitário de Saúde do SUS, que trabalha em rua sem sinal. Escreve local em
SQLite e sincroniza depois com padrão outbox, com retentativa e resolução de conflito. Nasceu de
iniciação científica e está incubado na Saruê, na UNESP Bauru.
[Demo](https://conectagente-web.vercel.app)

## Faculdade

Ciência da Computação na UNISAGRADO, 2024 a 2027. Trabalhos das disciplinas de Inteligência
Artificial, Processamento de Imagens e Sinais e Desenvolvimento de Jogos.

| Projeto | O que é |
|---|---|
| [PermaneIA](https://github.com/fabriciojunio/permaneia) | Assistente que responde só com base no material da disciplina, citando a fonte e admitindo quando não sabe, e painel de risco de evasão por lógica fuzzy. O motor de inferência de Mamdani foi escrito do zero, e a suíte tem 2.093 testes |
| [Cardiocam](https://github.com/fabriciojunio/cardiocam) | Frequência cardíaca medida por vídeo, sem encostar na pessoa. Quatro algoritmos da literatura comparados no mesmo pipeline |
| [Contaflux](https://github.com/fabriciojunio/contaflux) | Contagem de veículos em vídeo de câmera fixa, com a linha de contagem deduzida do próprio tráfego |
| [Kaida](https://github.com/fabriciojunio/kaida) | Metroidvania 2D em Unity, com o jogo inteiro montado por scripts de editor |
| [Bicudo](https://github.com/fabriciojunio/bicudo) | Jogo de um botão em Unity, individual |
| [Laboratório VR](https://github.com/fabriciojunio/LaboratorioVR) | Laboratório de química em realidade virtual, com interação por gaze |

## Código fechado

Produtos que já estão indo para cliente, então o repositório é privado.

**Balcão.** Atendimento de venda e troca de celular no WhatsApp. O modelo de linguagem não
escreve número: preço, parcela e valor de troca saem do domínio, e um auditor confere cada
algarismo antes de enviar. Node · TypeScript · Fastify · Prisma

**Horalis.** Apontamento de horas multiusuário com RBAC, controle de SLA e exportação em Excel.
Next.js · Prisma · JWT · [Demo](https://apontamento-horas.vercel.app)

**RegistraServiço.** Registro de prestação de serviço multi-tenant, em que a organização
configura os tipos e os campos em vez de o código trazer isso pronto. Next.js · Prisma ·
PostgreSQL · [Demo](https://registraservico.vercel.app)

**Guarda Banco.** Trava dentro do servidor de banco contra DELETE e UPDATE acidentais, por
limite de linhas afetadas por comando. Vale em qualquer cliente, do DBeaver ao psql.
PostgreSQL · PL/pgSQL · MySQL · SQL Server

## Outros

Projetos anteriores, que deixo públicos mas não são o que faço hoje:
[Paiol Tech](https://github.com/fabriciojunio/paiol-tech) (NestJS com CQRS e Open Finance),
[AuthCore](https://github.com/fabriciojunio/authcore) (JWT RS256, 2FA, RBAC),
[QuantBot ML](https://github.com/fabriciojunio/quantbot-ml) e
[GolData](https://github.com/fabriciojunio/goldata) (Python e ML),
[JIS](https://github.com/fabriciojunio/jis),
[KoraCRM](https://github.com/fabriciojunio/KoraCRM),
[MyCondPets](https://github.com/fabriciojunio/MyCondPets),
[Mente Viva](https://github.com/fabriciojunio/mente-viva),
[Mundo do Lukinha](https://github.com/fabriciojunio/mundo-do-lukinha).
