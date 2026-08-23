# Fabrício Júnio

Desenvolvedor back-end em Bauru/SP. Trabalho com Java, JavaScript e SQL sobre processos de
negócio que já estão rodando em empresa grande: integrações, automação e regra de negócio em
sistema vivo, com instâncias em andamento no momento em que a alteração sobe.

[LinkedIn](https://linkedin.com/in/fabríciojúnio) · [Portfólio](https://portfolio-a3qn.vercel.app) · junioad555@gmail.com

## O que eu faço

Hoje sou desenvolvedor na área de Serviços da Digihub Tecnologia, que faz parte do grupo Lecom.
A carteira é de treze clientes de seguros, saúde, cooperativismo de crédito, auditoria e
judiciário. Meu dia é receber um chamado, entender o processo, medir o que está acontecendo em
produção, propor a solução, desenvolver, homologar e publicar.

Na prática isso é integração e robô em Java, regra de tela em JavaScript sobre a API do
formulário da plataforma, roteamento de processo, SQL de diagnóstico e automação RPA.

O que eu levo para qualquer código que escrevo, dentro ou fora do trabalho: eu meço antes de
mexer. Reproduzo a regra atual, rodo contra o histórico real e só considero o modelo válido
quando ele acerta o passado. Se a simulação não prevê o que já aconteceu, ela não serve para
prever o que vai acontecer.

**Stack principal:** Java · Spring Boot · JavaScript · TypeScript · SQL · PostgreSQL · Docker
**Também uso:** Node/NestJS · Next.js · Python · React Native

## Projetos

Os que eu apresentaria numa entrevista, nesta ordem.

### [CodeReview AI](https://github.com/fabriciojunio/codereview-ai)
`Java 21 · Spring Boot 3.3 · RabbitMQ · Redis · PostgreSQL · Ollama`

Análise de código com modelo de linguagem rodando local, sem mandar código para API externa.
A submissão devolve um ticket e cai numa fila do RabbitMQ, o resultado volta por Server-Sent
Events conforme o modelo gera, e o Redis guarda 24h para que o mesmo código não seja analisado
duas vezes. É o projeto onde a decisão de arquitetura pesa mais que a funcionalidade.

### [Paiol Tech](https://github.com/fabriciojunio/paiol-tech)
`NestJS · CQRS · Turborepo · Next.js · PostgreSQL`

SaaS de gestão de dívidas rurais, monorepo com API e PWA. Separei comando de consulta com CQRS
porque o volume de leitura de posição consolidada não tem nada a ver com o de escrita de
lançamento. [Demo](https://paiol-tech.vercel.app)

### [AuthCore](https://github.com/fabriciojunio/authcore)
`Node · TypeScript · PostgreSQL · Redis · Docker`

Autenticação com JWT RS256, 2FA por TOTP, RBAC e registro de auditoria. Chave assimétrica para
que o serviço que valida o token não precise do segredo que o assina.
[Demo](https://frontend-tan-mu-38.vercel.app)

### [QuantBot ML](https://github.com/fabriciojunio/quantbot-ml)
`Python · XGBoost · PyTorch · FastAPI · GitHub Actions`

Carteira de dividendos que opera com dinheiro simulado, decide sozinha e roda todo dia na
nuvem. O que interessa aqui não é o retorno, é a disciplina: validação walk-forward, sem olhar
dado do futuro no treino, e pipeline que quebra o build quando o teste falha.

### [ConectAgente](https://github.com/fabriciojunio/ConectAgente)
`React Native · Expo · SQLite · Supabase`

App para Agente Comunitário de Saúde do SUS, que trabalha em rua sem sinal. Escreve local em
SQLite e sincroniza depois com padrão outbox, com retentativa e resolução de conflito. Nasceu
de iniciação científica e está incubado na Saruê, na UNESP Bauru. [Demo](https://conectagente-web.vercel.app)

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

Três produtos que já estão indo para cliente, então o repositório é privado.

**Balcão.** Atendimento de venda e troca de celular no WhatsApp. O modelo de linguagem não
escreve número: preço, parcela e valor de troca saem do domínio, e um auditor confere cada
algarismo antes de enviar. Node · TypeScript · Fastify · Prisma

**Horalis.** Apontamento de horas multiusuário com RBAC, controle de SLA e exportação em Excel.
Next.js · Prisma · JWT · [Demo](https://apontamento-horas.vercel.app)

**RegistraServiço.** Registro de prestação de serviço multi-tenant, em que a organização
configura os tipos e os campos em vez de o código trazer isso pronto. Next.js · Prisma ·
PostgreSQL · [Demo](https://registraservico.vercel.app)

## Outros

Projetos anteriores, que deixo públicos mas não são o que eu faço hoje:
[GolData](https://github.com/fabriciojunio/goldata) e
[GolData Pro](https://github.com/fabriciojunio/bot-sinais) (analytics de futebol com ML),
[JIS](https://github.com/fabriciojunio/jis) (agregador de vagas),
[KoraCRM](https://github.com/fabriciojunio/KoraCRM) (CRM em Laravel),
[MyCondPets](https://github.com/fabriciojunio/MyCondPets),
[Mente Viva](https://github.com/fabriciojunio/mente-viva),
[Mundo do Lukinha](https://github.com/fabriciojunio/mundo-do-lukinha).
