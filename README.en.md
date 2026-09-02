# Fabrício Júnio

*[Leia em português](README.md)*

Backend developer in Bauru, Brazil. Java and Spring Boot, integration work, and systems that talk
to each other over events. At work, business processes that are already running inside large
companies, with instances in flight at the moment a change goes out.

[LinkedIn](https://linkedin.com/in/fabríciojúnio) · [Portfolio](https://portfolio-a3qn.vercel.app) · junioad555@gmail.com

## What I do

I work in the services team at Digihub Tecnologia, part of the Lecom group, on a portfolio of
thirteen clients across insurance, healthcare, credit unions, auditing and the judiciary. The day
is: take a ticket, understand the process, measure what is actually happening in production,
propose, build, get it validated, ship. In practice that means integrations and scheduled jobs in
Java, screen rules in JavaScript, process routing, diagnostic SQL, and RPA automation.

The habit that came out of that and now goes into everything I write: I measure before I touch.
I reproduce the current rule as it is stored, run it against real history, and only trust the
model once it gets the past right. If a simulation cannot predict what already happened, it is
not going to predict what comes next.

**Stack:** Java 21 · Spring Boot · Kafka · SQL · PostgreSQL · Docker · Kubernetes · AWS
**Also use:** Node/NestJS · TypeScript · Next.js · Python

## Projects

### [Feira do Comando](https://github.com/fabriciojunio/feira-do-comando)
`Java 21 · Spring Boot · Kafka · PostgreSQL · MongoDB · Terraform · Kubernetes`

Event-driven order platform. Four services, each owning its database, none reading another's
tables. The saga has to survive messages that arrive twice, out of order and late, and the case
that took the most work is the race where payment is approved while cancellation is already under
way. Transactional outbox with `SELECT FOR UPDATE SKIP LOCKED` so it runs on several instances,
and consumers made idempotent through an inbox. Concurrency is proven with ten real threads
against a real PostgreSQL rather than with a simulation: 108 orders per second, printed into the
build output. Infrastructure is described in Terraform, with a VPC of private subnets, RDS, ECR
and managed Kafka.

### [Vitrine Bauru](https://github.com/fabriciojunio/vitrine-bauru)
`Java 21 · Spring Boot · Kafka · Amazon SNS/SQS · PostgreSQL · React 19`

Live, built with the economic development department of the city of Bauru. Event transport is one
interface with three adapters: Kafka where a broker exists, Amazon SNS on the managed deployment,
and an in-process call when there is no broker at all. Swapping the transport changes the network
without touching the guarantees. Data erasure under Brazil's LGPD is a saga with a deadline and
retries, where three services have to confirm before the request can close. 1,042 tests that boot
embedded PostgreSQL and embedded Kafka without needing Docker installed.
[Live](https://vitrine-bauru.vercel.app)

### [Outorga](https://github.com/fabriciojunio/outorga)
`Java · Spring Boot · Next.js · PostgreSQL`

White-label multi-tenant streaming where the broadcast licence is a domain invariant: there is no
code path that publishes content without one. The rule does not live in an `if` inside a
controller, it lives where it cannot be routed around.

### [CodeReview AI](https://github.com/fabriciojunio/codereview-ai)
`Java 21 · Spring Boot · RabbitMQ · Redis · PostgreSQL · Ollama`

Code review with a language model running locally, so the code never leaves the network.
Submission returns a ticket and goes onto a queue; the result comes back over Server-Sent Events
as the model generates it, and Redis caches for 24 hours keyed by the code hash. 88 tests, the
integration ones on Testcontainers.

### [ConectAgente](https://github.com/fabriciojunio/ConectAgente)
`React Native · Expo · SQLite · Supabase`

An app for community health workers in Brazil's public health system, who work on streets with no
signal. It writes locally to SQLite and syncs later using the outbox pattern, with retries and
conflict resolution. It started as undergraduate research and is incubated at Saruê, UNESP Bauru.
[Demo](https://conectagente-web.vercel.app)

## University

Computer Science at UNISAGRADO, 2024 to 2027. Coursework from Artificial Intelligence, Image and
Signal Processing, and Game Development.

| Project | What it is |
|---|---|
| [PermaneIA](https://github.com/fabriciojunio/permaneia) | A study assistant that answers only from the course material, cites the source and admits when it does not know, plus a dropout-risk panel using fuzzy logic. The Mamdani inference engine was written from scratch, and the suite has 2,093 tests |
| [Cardiocam](https://github.com/fabriciojunio/cardiocam) | Heart rate measured from video without touching the person. Four algorithms from the literature compared in the same pipeline |
| [Contaflux](https://github.com/fabriciojunio/contaflux) | Vehicle counting from fixed-camera video, with the counting line inferred from the traffic itself |
| [Kaida](https://github.com/fabriciojunio/kaida) | 2D metroidvania in Unity, with the whole game assembled by editor scripts |
| [Bicudo](https://github.com/fabriciojunio/bicudo) | One-button game in Unity, solo |
| [Laboratório VR](https://github.com/fabriciojunio/LaboratorioVR) | A chemistry lab in virtual reality, with gaze interaction |

## Closed source

Products already going to clients, so the repositories are private.

**Balcão.** Phone sales and trade-ins handled over WhatsApp. The language model does not write
numbers: price, instalment and trade-in value come from the domain, and an auditor checks every
digit before the message goes out. Node · TypeScript · Fastify · Prisma

**Horalis.** Multi-user time tracking with RBAC, SLA control and Excel export. Next.js · Prisma ·
JWT · [Demo](https://apontamento-horas.vercel.app)

**RegistraServiço.** Multi-tenant service records where the organisation configures the types and
the fields instead of the code shipping them hard-coded. Next.js · Prisma · PostgreSQL ·
[Demo](https://registraservico.vercel.app)

**Guarda Banco.** A guard inside the database server against accidental DELETE and UPDATE, based
on a row limit per statement. Works from any client, from DBeaver to psql. PostgreSQL · PL/pgSQL ·
MySQL · SQL Server

## Older work

Public, but not what I do now:
[Paiol Tech](https://github.com/fabriciojunio/paiol-tech) (NestJS with CQRS and Open Finance),
[AuthCore](https://github.com/fabriciojunio/authcore) (JWT RS256, 2FA, RBAC),
[QuantBot ML](https://github.com/fabriciojunio/quantbot-ml) and
[GolData](https://github.com/fabriciojunio/goldata) (Python and ML),
[JIS](https://github.com/fabriciojunio/jis),
[KoraCRM](https://github.com/fabriciojunio/KoraCRM),
[MyCondPets](https://github.com/fabriciojunio/MyCondPets),
[Mente Viva](https://github.com/fabriciojunio/mente-viva),
[Mundo do Lukinha](https://github.com/fabriciojunio/mundo-do-lukinha).
