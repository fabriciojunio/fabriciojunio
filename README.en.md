# Fabrício Júnio

*[Leia em português](README.md)*

Backend and machine learning, based in Bauru, Brazil. Java and Spring Boot for the service that
ships, Python and statistics when the problem is deciding under uncertainty. The part I care about
is in between: where a model stops being a number in a notebook and becomes a decision someone
has to sign off on.

[LinkedIn](https://linkedin.com/in/fabríciojúnio) · [Portfolio](https://fabriciojunio.vercel.app) · junioad555@gmail.com

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
**Models and data:** Python · numpy · pandas · scikit-learn · OpenCV · applied statistics
**Also use:** Node/NestJS · TypeScript · Next.js

## Models and decisions

Projects where the output is a number somebody acts on. In all of them the measurement protocol
sits in the repository next to the code, because a number without its protocol is worth nothing.

### Lastro
`Python · numpy · multi-objective evolutionary search` · *private repository until the defence*

My final-year project. It learns the dependency structure between 22 Brazilian financial
institutions listed on the B3 exchange as a Gaussian Bayesian network, searched with a
multi-objective evolutionary algorithm that returns the whole frontier between fit and edge count.
Data: 3,471 trading days from 2012 to 2025, straight from the exchange's raw historical files,
with 9 corporate events detected and audited one by one. Tickers that stopped trading stay in the
sample for as long as they existed, so the selection rule does not create survivorship bias.

The average network is checkable by anyone who knows the sector: ITSA4 and ITUB4 appear together
in 154 out of 154 windows, because Itaúsa is the holding company that controls Itaú. The half-life
of the structure is 742 trading days, about three years, 95% interval from 638 to 874.

Of four research questions, two were answered "no", and both are written up in the same detail as
the other two. Validation against known structures failed the first version of the learner, with
the gap growing in the number of vertices (Friedman, p = 6.5 × 10⁻¹¹). The diagnosis changed the
algorithm: once the topological order is fixed, the edge mask does not have to be searched, it
**can be computed** node by node, because the score is decomposable and acyclicity is already
guaranteed by the order. Fed the true order, SHD drops to 4, 5 and 7 at ten, twenty and thirty
vertices. Had the project skipped that phase, the worse version would have gone on to market data
and nothing in the result would have given it away.

### [Anteparo](https://github.com/fabriciojunio/anteparo)
`Python · scikit-learn · numpy`

Expected credit loss provisioning under IFRS 9 and Brazil's CMN Resolution 4,966. The arithmetic
is `ECL = PD × LGD × EAD`; the work is deciding which PD goes into it. On the test set, touched
exactly once, the chosen model reaches a Gini of 0.542 with an expected-over-observed ratio of
0.991, and beats the rule a credit team would build in a spreadsheet by 1.51x. The selection
criterion is not the highest Gini: it is the highest Gini among candidates whose calibration error
is within twice the best, because provisioning uses the probability as a number, not as a ranking.

The most important result is not about the model. Provisioning moves by 1.45x just from changing
the LGD assumption inside the declared range, considerably more than the distance between the best
and the worst PD algorithm. Arguing about which algorithm to use while LGD is a guess is arguing
about the wrong part of the problem.

Dropping sex, education and marital status costs −0.0024 Gini, meaning the model is marginally
**better** without them. And the finding the aggregate metric hides: in a group of 91 cases the
model overstates risk by a factor of nearly five, with an AUC worse than chance.

### [Baliza](https://github.com/fabriciojunio/baliza)
`Python · OpenCV · YOLO11`

Parking space occupancy from camera footage. Two routes live in the same project, both measured on
the same camera neither of them saw during training: the classical image-processing detector is
86.5% accurate at 34 ms per image on CPU, and YOLO is 97.5% accurate at 5.3 s. The classical one
loses 10.9 points, almost all of it in recall, and runs 155 times faster. That trade-off is what
decides what goes onto an edge device with no GPU, and it only shows up because both were measured
on the same images at the same resolution.

The classical detector's threshold is not eyeballed: it is calibrated on two cameras and measured
on a third. Two decisions changed the outcome, and both were mistakes before they were fixes:
standardising per camera rather than globally, and picking the threshold by F1 rather than by
accuracy.

### [PermaneIA](https://github.com/fabriciojunio/permaneia)
`Python · FastAPI · fuzzy logic`

A study assistant that answers only from the course material, cites the source and admits when it
does not know, plus a dropout-risk panel using fuzzy logic. The Mamdani inference engine was
written from scratch, with 2,093 tests. [Live](https://permaneia.vercel.app)

### [Cardiocam](https://github.com/fabriciojunio/cardiocam)
`Python · OpenCV · scipy`

Heart rate measured from video without touching the person. Four algorithms from the literature
compared in the same pipeline, so that differences between them are not differences in
implementation. [Live](https://cardiocam.vercel.app)

### [Contaflux](https://github.com/fabriciojunio/contaflux)
`Python · OpenCV`

Vehicle counting from fixed-camera video, with the counting line inferred from the traffic itself
rather than drawn by hand. Two detectors, and a published executable.

## Partnerships

### [Vitrine Bauru](https://github.com/fabriciojunio/vitrine-bauru)
`Java 21 · Spring Boot · Kafka · Amazon SNS/SQS · PostgreSQL · React 19`

Live, built with the economic development department of the city of Bauru. Event transport is one
interface with three adapters: Kafka where a broker exists, Amazon SNS on the managed deployment,
and an in-process call when there is no broker at all. Swapping the transport changes the network
without touching the guarantees. Distributed tracing survives the outbox: the `traceparent` goes
into a column and then into a header, otherwise the context dies at commit and the dashboard
shows two disconnected traces instead of one whole request. Data erasure under Brazil's LGPD is a
saga with a deadline and retries, where three services have to confirm before the request can
close. 1,042 tests that boot embedded PostgreSQL and embedded Kafka without needing Docker
installed. [Live](https://vitrine-bauru.vercel.app)

### [ConectAgente](https://github.com/fabriciojunio/ConectAgente)
`React Native · Expo · SQLite · Supabase`

An app for community health workers in Brazil's public health system, who work on streets with no
signal. It writes locally to SQLite and syncs later using the outbox pattern, with retries and
conflict resolution. It started as undergraduate research and is incubated at Saruê, UNESP Bauru.
[Demo](https://conectagente-web.vercel.app)

## Backend and product

### [Feira do Comando](https://github.com/fabriciojunio/feira-do-comando)
`Java 21 · Spring Boot · Kafka · PostgreSQL · MongoDB · Terraform · Kubernetes`

Event-driven order platform. Four services, each owning its database, none reading another's
tables. The saga has to survive messages that arrive twice, out of order and late, and the case
that took the most work is the race where payment is approved while cancellation is already under
way. Transactional outbox with `SELECT FOR UPDATE SKIP LOCKED` so it runs on several instances,
and consumers made idempotent through an inbox. Concurrency is proven with ten real threads
against a real PostgreSQL rather than with a simulation: 108 orders per second, printed into the
build output. Infrastructure is described in Terraform, with a VPC of private subnets, RDS, ECR
and managed Kafka. Distributed tracing survives the outbox, and a k6 load test measures the
system over a real network rather than just the code in-process.

### [Outorga](https://github.com/fabriciojunio/outorga-tv)
`Java · Spring Boot · Next.js · PostgreSQL`

White-label multi-tenant streaming where the broadcast licence is a domain invariant: there is no
code path that publishes content without one. The rule does not live in an `if` inside a
controller, it lives where it cannot be routed around.

### [CodeReview AI](https://github.com/fabriciojunio/codereview-ai)
`Java 21 · Spring Boot · RabbitMQ · Redis · PostgreSQL · Ollama`

Code review with a language model running locally, so the code never leaves the network.
Submission returns a ticket and goes onto a queue; the result comes back over Server-Sent Events
as the model generates it, and Redis caches for 24 hours keyed by the code hash. It accepts both
its own login and a token from an external identity provider, because inside a company
authentication comes from the Keycloak or Entra ID the identity team already runs. The cache uses
jittered TTLs against expiry stampedes, and a processing lease so ten identical submissions do not
become ten inferences. 112 tests, with a coverage gate enforced in the build.

### Closed source

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

## University

Computer Science at UNISAGRADO, 2024 to 2027. The Artificial Intelligence and Image and Signal
Processing coursework is up above, alongside the rest of what I do in that area. What is left here
is Game Development and Virtual Reality.

| Project | What it is |
|---|---|
| [Kaida](https://github.com/fabriciojunio/kaida) | 2D metroidvania in Unity, with the whole game assembled by editor scripts |
| [Bicudo](https://github.com/fabriciojunio/bicudo) | One-button game in Unity, solo |
| [Laboratório VR](https://github.com/fabriciojunio/LaboratorioVR) | A chemistry lab in virtual reality, with gaze interaction |

<details>
<summary><b>Older work</b> (public, but not what I do now)</summary>

<br>

| Project | What it is |
|---|---|
| [Paiol Tech](https://github.com/fabriciojunio/paiol-tech) | NestJS with CQRS and Open Finance |
| [AuthCore](https://github.com/fabriciojunio/authcore) | Authentication with JWT RS256, 2FA and RBAC |
| [GolData](https://github.com/fabriciojunio/goldata) | Signal engine in Python |
| [JIS](https://github.com/fabriciojunio/jis) | Job aggregator in Next.js, eight real sources |
| [KoraCRM](https://github.com/fabriciojunio/KoraCRM) | CRM in PHP and Laravel |
| [Almanaque](https://github.com/fabriciojunio/almanaque) | Local guide and classifieds in Symfony, with a support console |
| [MyCondPets](https://github.com/fabriciojunio/MyCondPets) | Pet registry for apartment buildings |
| [Mente Viva](https://github.com/fabriciojunio/mente-viva) | Study support application |
| [Mundo do Lukinha](https://github.com/fabriciojunio/mundo-do-lukinha) | Children's site |

</details>
