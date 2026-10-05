# Fabrício Júnio

*[Read this in English](README.en.md)*

IA aplicada a risco, crédito e decisão, em Bauru/SP. Python e estatística quando o problema é
decidir com dado incerto, Java e Spring Boot no serviço que vai para produção. A parte que me
interessa é a do meio: onde o modelo deixa de ser um número num caderno e passa a ser uma decisão
que alguém assina.

[LinkedIn](https://linkedin.com/in/fabríciojúnio) · [Portfólio](https://fabriciojunio.vercel.app) · junioad555@gmail.com

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
**Modelo e dado:** Python · numpy · pandas · scikit-learn · OpenCV · estatística aplicada
**Também uso:** Node/NestJS · TypeScript · Next.js

## Modelo e decisão

Projetos em que a saída é um número que alguém usa para decidir. Em todos eles o protocolo de
medição está no repositório junto com o código, porque o número sem o protocolo não vale nada.

### Lastro
`Python · numpy · algoritmo evolutivo multiobjetivo` · *repositório privado até a defesa*

Trabalho de conclusão de curso. Aprende a estrutura de dependência entre 22 instituições
financeiras da B3 como rede bayesiana gaussiana, com a busca feita por um evolutivo multiobjetivo
que devolve a fronteira inteira entre ajuste e número de arestas. Base: 3.471 pregões de 2012 a
2025, direto do COTAHIST, com 9 eventos corporativos detectados e auditados um por um, e os papéis
que deixaram de ser negociados permanecem na amostra enquanto existiram, para não criar viés de
sobrevivência.

A rede média dá para conferir no olho de quem conhece o setor: ITSA4 e ITUB4 aparecem juntas em
154 das 154 janelas, porque a Itaúsa controla o Itaú. A meia-vida da estrutura é de 742 pregões,
cerca de três anos, com intervalo de 95% entre 638 e 874.

De quatro perguntas, duas foram respondidas com "não", e as duas estão no texto com o mesmo
detalhe das outras. A validação contra estruturas conhecidas reprovou a primeira versão do
aprendiz, com a diferença crescendo junto com o número de vértices. O diagnóstico mudou o
algoritmo: fixada a ordem topológica, a máscara de arestas não precisa ser procurada, ela
**se calcula** nó a nó, porque a pontuação é decomponível e a aciclicidade já está garantida.

Com a correção, o aprendiz passou ao primeiro posto médio entre sete algoritmos nas mesmas 840
execuções (Friedman, p = 9,3 × 10⁻¹⁵). Ganha da busca tabu e da escalada de colina com tamanho de
efeito alto, e **empata com o PC**, o que está escrito como empate e não como vitória. O teto da
codificação está medido à parte: com a ordem topológica verdadeira o erro estrutural cai para
7,07, contra 40,38 de uma ordem sorteada, e ordenar por variância marginal, que é a heurística
plausível, fica em 12,25. Se o trabalho tivesse pulado essa fase, a versão pior teria ido para o
dado de mercado e nada no resultado teria denunciado.

### [Anteparo](https://github.com/fabriciojunio/anteparo)
`Python · scikit-learn · numpy`

Provisão para perda esperada de crédito sob IFRS 9 e Resolução CMN 4.966. A conta é
`ECL = PD × LGD × EAD`; o trabalho está em decidir qual PD entra nela. No teste, tocado uma única
vez, o modelo escolhido faz Gini de 0,542 com esperado sobre observado de 0,991, e ganha 1,51x da
regra que uma área de crédito montaria numa planilha. O critério de escolha não é o maior Gini:
é o maior Gini entre os candidatos cujo erro de calibração está dentro do dobro do melhor, porque
provisão usa a probabilidade como número e não como ordem.

O resultado mais importante não é do modelo. A provisão varia 1,45x só mudando a hipótese de LGD
dentro da faixa declarada, bem mais do que a distância entre o melhor e o pior algoritmo de PD.
Discutir qual modelo usar enquanto a LGD é um chute é discutir a parte errada do problema.

Tirar sexo, escolaridade e estado civil custa −0,0024 de Gini, ou seja, o modelo fica
marginalmente melhor sem elas. E o achado que a métrica agregada esconde: num grupo de 91 casos,
o modelo superestima o risco por um fator de quase cinco, com AUC pior que o acaso.

### [Prumo](https://github.com/fabriciojunio/prumo)
`Python · pandas · SciPy`

O desempenho passado de um fundo prevê o futuro? Medido em 42,3 milhões de linhas
de cota diária da CVM, com 40.961 séries de 2018 a 2025. A resposta é "quase
nada, e depende da classe": renda fixa persiste de verdade, com razão de chances
de 3,82, e ações não persiste, com 0,94 e o intervalo encostando em 1 pelo lado
de cima.

Em dinheiro não vale nada: a diferença entre o melhor e o pior quintil é de 0,72%
no ano seguinte, contra 19,20% de dispersão dentro de cada quintil. Vinte e seis
vezes maior.

O achado que não estava no roteiro é que a matriz de transição é em U. Do quintil
pior, 30,0% ficam e 29,6% vão direto para o melhor. Quem está nas pontas é o
fundo volátil, e o que persiste de um ano para o outro é o **risco**, não o
retorno. O viés de sobrevivência está medido: só 19% das séries existem do início
ao fim do período.

### [Verbete](https://github.com/fabriciojunio/verbete)
`Python · scikit-learn · pandas`

Classifica projeto de lei pelos 32 temas oficiais da Câmara, a partir da ementa.
O resultado principal é o tamanho do vazamento de anotação: o campo de
palavras-chave da API é preenchido pela mesma indexação humana que atribui o
tema, e usá-lo leva o micro-F1 de 0,542 para 0,682. Um modelo que o usasse
pareceria 26% melhor do que vai ser quando a proposição chegar sem indexação
nenhuma.

A resposta de produto é negativa e está escrita: o alvo de 0,70 de micro-F1 não é
alcançado em cobertura nenhuma. A divisão é temporal e não aleatória, porque
proposição sobre o mesmo assunto reaparece a cada legislatura com ementa quase
igual. O classificador é linear de propósito: num setor regulado, explicação que
não vem do modelo que decidiu é uma segunda opinião.

### [Trato](https://github.com/fabriciojunio/trato)
`Python · scikit-learn · SciPy`

Quem contatar, e não quem vai pagar. Modelagem de uplift num experimento
aleatorizado de verdade, com 64 mil pessoas e 21 mil no controle.

O que mais vale no projeto vem antes do modelo: ele mede se existe
heterogeneidade para achar, calculando o efeito dentro de 19 subgrupos conhecidos
de antemão, sem modelo nenhum. Num braço do experimento nenhuma fatia difere do
efeito geral, e os modelos confirmam sem separar nada. O resultado negativo está
correto, e isso só dá para afirmar porque a heterogeneidade foi medida em
separado. No outro braço ela existe, é interpretável, e o modelo encontra:
separação de 3x entre topo e fundo, e 11,6% a mais de resultado contatando 25
pontos percentuais menos gente.

Uplift não tem rótulo individual, porque ninguém é observado contatado e não
contatado ao mesmo tempo. Toda a validação é por grupo, e essa ausência de
métrica individual é deliberada.

### [Decurso](https://github.com/fabriciojunio/decurso)
`Python · pandas · scikit-learn · SciPy`

Quanto um processo judicial dura, e quanto disso vira provisão pelo critério do
CPC 25. A conta que sai de planilha, a média dos processos já encerrados,
descarta 20,8% da base e erra para baixo por 1,21x: 791 dias contra 955 da
mediana de Kaplan-Meier. O erro não é aleatório, e é maior justamente na vara
mais lenta.

O modelo de desfecho dá resultado negativo e está relatado como tal: AUC de
0,521, sem diferença significativa nem contra a taxa global nem contra a taxa do
órgão. E um achado morreu quando a amostra cresceu: com 2.648 processos a
diferença sobrevivia à correção de Benjamini-Hochberg, com 4.118 ela não
sobrevive mais. Está escrito no relatório em vez de apagado.

A hipótese de valor em risco move a provisão 4,00x, contra 1,09x da escolha do
modelo.

O comportamento da API pública do CNJ foi medido, não presumido: ordenação
devolve 504 em qualquer forma, o que inviabiliza `search_after`, e a contagem
sem `track_total_hits` para em 10.000, fazendo uma consulta de 300 mil processos
parecer uma de 10 mil. O coletor divide o período até cada fatia caber e grava o
que faltou, fatia por fatia. 142 testes, nenhum deles tocando a API.

### [Baliza](https://github.com/fabriciojunio/baliza)
`Python · OpenCV · YOLO11`

Ocupação de vaga de estacionamento por câmera. São dois caminhos no mesmo projeto, medidos na
mesma câmera que nenhum dos dois viu em treino: o detector clássico de processamento de imagens
acerta 86,5% gastando 34 ms por imagem na CPU, e o YOLO acerta 97,5% gastando 5,3 s. O clássico
perde 10,9 pontos, quase tudo em revocação, e roda 155 vezes mais rápido. É essa troca que decide
o que vai para um equipamento de borda sem GPU, e ela só aparece porque os dois foram medidos nas
mesmas imagens e na mesma resolução.

O limiar do clássico não é escolhido no olho: calibra em duas câmeras e mede na terceira. Duas
decisões mudaram o resultado e as duas foram erro antes de virarem acerto, padronizar por câmera
em vez de globalmente e escolher o limiar por F1 em vez de acurácia.

### [PermaneIA](https://github.com/fabriciojunio/permaneia)
`TypeScript · Next.js · PostgreSQL · lógica fuzzy`

Assistente que responde só com base no material da disciplina, citando a fonte e admitindo quando
não sabe, e painel de risco de evasão por lógica fuzzy. A recuperação é híbrida, vetorial mais
casamento de termo, e o limiar que decide entre responder e recusar foi calibrado contra uma
bateria de 52 perguntas: 41 que o material responde, 8 que ele não responde e 3 que devem ser
respondidas com o aviso de que não há fonte. No chute inicial de 0,62 a recusa correta era de
37,5%. O motor de inferência de Mamdani foi escrito do zero, com 2.041 testes.
[No ar](https://permaneia.vercel.app)

### [Cardiocam](https://github.com/fabriciojunio/cardiocam)
`Python · OpenCV · scipy`

Frequência cardíaca medida por vídeo, sem encostar na pessoa. Quatro algoritmos da literatura
comparados no mesmo pipeline, para que a diferença entre eles não vire diferença de
implementação. [No ar](https://cardiocam.vercel.app)

### [Contaflux](https://github.com/fabriciojunio/contaflux)
`Python · OpenCV`

Contagem de veículos em vídeo de câmera fixa, com a linha de contagem deduzida do próprio
tráfego em vez de desenhada à mão. Dois detectores e um executável publicado.

## Parceria e extensão

### [Vitrine Bauru](https://github.com/fabriciojunio/vitrine-bauru)
`Java 21 · Spring Boot · Kafka · Amazon SNS e SQS · PostgreSQL · React 19`

No ar, em parceria com a Secretaria de Desenvolvimento Econômico de Bauru. O transporte de
eventos é uma interface com três adaptadores: Kafka onde existe corretor, Amazon SNS na
implantação gerenciada, e entrega dentro do próprio processo quando não há corretor nenhum.
Trocar o transporte muda a rede sem mexer nas garantias. O rastro distribuído atravessa o
outbox: o `traceparent` vai numa coluna e depois em cabeçalho, senão o contexto morre no commit e
o painel mostra dois rastros desligados no lugar de um pedido inteiro. A exclusão de dados pela
LGPD é uma saga com prazo e reenvio, em que três serviços precisam confirmar antes de o pedido
fechar. 1.042 testes que sobem PostgreSQL e Kafka embarcados, sem exigir Docker instalado.
[No ar](https://vitrine-bauru.vercel.app)

### [ConectAgente](https://github.com/fabriciojunio/ConectAgente)
`React Native · Expo · Next.js · PostgreSQL`

App para Agente Comunitário de Saúde do SUS, que trabalha em rua sem sinal. Escreve local e
sincroniza depois, com retentativa e resolução de conflito. Nasceu de iniciação científica e está
incubado na Saruê, na UNESP Bauru. O desenvolvimento é em equipe e o repositório do time é o
endereço acima.
[Demo](https://conectagente-web.vercel.app)

## Back-end e produto

### [Feira do Comando](https://github.com/fabriciojunio/feira-do-comando)
`Java 21 · Spring Boot · Kafka · PostgreSQL · MongoDB · Terraform · Kubernetes`

Pedidos orientados a eventos. Quatro serviços com banco próprio, nenhum lendo tabela do outro.
A saga precisa sobreviver a mensagem repetida, fora de ordem e atrasada, e o caso que mais deu
trabalho foi a corrida em que o pagamento é aprovado durante o cancelamento. Outbox transacional
com `SELECT FOR UPDATE SKIP LOCKED`, para rodar em várias instâncias, e consumidor idempotente
pelo inbox. Concorrência provada com dez threads reais contra um PostgreSQL real, não com
simulação: 108 pedidos por segundo, impressos na saída do build. A infraestrutura está em
Terraform, com VPC de sub-rede privada, RDS, ECR e Kafka gerenciado.

### [Outorga](https://github.com/fabriciojunio/outorga-tv)
`Java · Spring Boot · Next.js · PostgreSQL`

Streaming white-label multi-tenant em que a licença de exibição é invariante de domínio: não
existe caminho de código que publique conteúdo sem ela. A regra não fica num `if` do
controlador, fica no lugar onde não dá para desviar.

### [CodeReview AI](https://github.com/fabriciojunio/codereview-ai)
`Java 21 · Spring Boot · RabbitMQ · Redis · PostgreSQL · Ollama`

Análise de código com modelo de linguagem rodando local, então o código não sai da rede. A
submissão devolve um ticket e cai numa fila, o resultado volta por Server-Sent Events conforme o
modelo gera, e o Redis guarda 24h pelo hash do código. Aceita tanto o login próprio quanto token
de um provedor de identidade externo, porque numa empresa a autenticação vem do Keycloak ou do
Entra ID que o time de identidade já opera. O cache tem prazo variável, contra a rajada de
vencimentos simultâneos, e reserva de análise, para dez submissões do mesmo código não virarem
dez inferências. 112 testes, com o gate de cobertura travado no build.

### Código fechado

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

## Faculdade

Ciência da Computação na UNISAGRADO, 2024 a 2027. Os trabalhos de Inteligência Artificial e de
Processamento de Imagens e Sinais estão lá em cima, junto com o resto do que faço na área. Aqui
ficam os de Desenvolvimento de Jogos e Realidade Virtual.

| Projeto | O que é |
|---|---|
| [Kaida](https://github.com/fabriciojunio/kaida) | Metroidvania 2D em Unity, com o jogo inteiro montado por scripts de editor |
| [Bicudo](https://github.com/fabriciojunio/bicudo) | Jogo de um botão em Unity, individual |
| [Laboratório VR](https://github.com/fabriciojunio/LaboratorioVR) | Laboratório de química em realidade virtual, com interação por gaze |

<details>
<summary><b>Outros projetos</b> (anteriores, públicos, não são o que faço hoje)</summary>

<br>

| Projeto | O que é |
|---|---|
| [Paiol Tech](https://github.com/fabriciojunio/paiol-tech) | NestJS com CQRS e Open Finance |
| [AuthCore](https://github.com/fabriciojunio/authcore) | Autenticação com JWT RS256, 2FA e RBAC |
| [JIS](https://github.com/fabriciojunio/jis) | Agregador de vagas em Next.js, oito fontes reais |
| [KoraCRM](https://github.com/fabriciojunio/KoraCRM) | CRM em PHP e Laravel |
| [Almanaque](https://github.com/fabriciojunio/almanaque) | Guia e classificados em Symfony, com console de suporte |

</details>
