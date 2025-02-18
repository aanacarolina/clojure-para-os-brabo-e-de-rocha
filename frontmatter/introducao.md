# Introducao

No mais profundo do seu ser, voce sempre soube que estava predestinada a aprender Clojure. Todas as vezes que voce segurou seu teclado , chorando de desespero por cause de uma hieraquia de classe incompreensivel; todas as vezes que voce ficou a noite toda acordada , enchendo o saco das suas pessoas queridas chorando por causa de um heisenbug induzido por mutacao; toda as vezes que uma (race condition) te levou a puxar, os seus ja ralos, cabelos, uma parte secreta sua ja sabia que teria que existir um caminho melhor.

Agora, finalmente, o material de instrucao que voce tem bem na sua frente vai te unir com a linguagem de programacao que voce tanto esperou.

# Aprendendo uma Nova Linguagem de Programacao: Uma Jornada pelos Quatro Labirintos

Para tirar maximo proveito do Clojure, voce tera que encontrar o seu caminho atraves dos quatro labirintos que todo programador se encontra quando esta aprendendo uma nova linguagem:

- **A Floresta das Ferramentas:** Um ambiente amigavel e eficiente que facilita voce experimentar suas ideias. Voce ira aprender a configurar seu ambiente.

- **A Montanha das Linguagens:** Enquanto voce a escala, voce ganhara conhecimento da sintaxe, semantica e estrutura de dados do Clojure. Voce ira aprender como usar uma das mais poderosas ferramentes de programacao, a macro, e aprendera a simplicar sua vida com as construcoes de concorrencia do Clojure.

- **A Caverna dos Artifatos:** Nas suas profundezas voce ira aprendar construir (buildar?), executar e distribuir seus proprios programas e como usar bibliotecas de codigo. Voce tambem irá aprender a relacao do Clojure com a JVM (Java Virtual Machine -  Máquina Virtual do Java).

- **O Castelo de Nuvem da Mentalidade:** No seu ar rarefeito, voce virá a saber o porquê e o como do Lisp e programacao funcional. Voce ira aprendar a filosofia da simplicidade que permeia o Clojure e como resolver problemas como uma Clojurista. 

Não se engane, voce terá que dar duro. Mas este livro vai fazer o trabalho ser estimulante, e nao exaustivo. Isso porque o livro segue tres diretrizes:

- Ele usa a abordagem de oferecer a sobremese antes, fornecendo as ferramentas e os detalhes da linguagem que voce precisa para comecar logo a brincar com programas de verdade.

- Ele supoe que voce tenha zero experiencia com a JVM, programacao funcional ou LISP. Ele cobre detalhes de forma que voce se sentira confiante em relacao ao que voce estiver fazendo quando construir (buildar?) e executar programas em Clojure.

- Ele evita exemplos do mundo real em beneficio de atividades mais interessantes, tipo atacar hobbits e perseguir vampiros purpurinados.

Ao chegar no final do livro, voce sera capaz de usar Clojure, uma das mais empolgantes e divertidas linguagens de programacao que existe!

# Como este livro esta organizado?

Este livro está dividido em tres partes, para melhor te guiar na sua valorosa busca, corajosos novatos Clojuristas.

## Parte I
Para ficar motivada e aprender eficientemente, voce ira precisar escrever codigos e executaveis de verdade. Esses capitulos irao te levar num breve tour pelas ferramentos que voce precisará para escriver programas mais facilmente. Dessa maneira voce podera focar em aprender Clojure e nao ficar mexendo com seu ambiente.

### *Capítulo 1: Construindo (buildando?), Executando e o REPL*

Ha algo poderoso e motivador em fazer um programa de verdade rodar. Uma vez que voce consegue fazer isso, voce esta livre para experimentar, e de fato poder compartilhar o seu trabalho!

Nesse curto capitulo, voce ira investir um pouco de tempo para se familiarizar com uma rapida maneira de construir e executar programas em Clojure. Voce ira aprender como experimentar? como o codio sendo executado em um processo Clojure usando o REPL (o loop read-eval-print - ler-avaliar-imprimir). Isso ira estreitar o seu ciclo de feedback e te ajudar a aprender de forma mais eficiente.


### *Capítulo 2: Como usar o Emacs, um otimo editor de codigo para Clojure*

Ter um curto ciclo de feedback é crucial para o aprendizado. Neste capitulo irei cobrir Emacs desde a sua base para garantir que voce tem um fluxo de trabalho eficiente de Emacs/Clojure 

## Parte II - Fundamentos da Linguagem
Esses capitulos irao te dar uma base solida para seguir aprendendo Clojure. Você começará aprendendo os conceitos básicos do Clojure (sintaxe, semântica e estruturas de dados) de forma a poder fazer algumas coisas. Então, você dará um passo para trás para examinar em detalhes as funções mais usadas do Clojure e aprenderá como resolver problemas com elas usando a mentalidade da programação funcional.

### *Capítulo 3: Faça coisas: Intensivão de Clojure*
É aqui que você começará a realmente se aprofundar no Clojure. É também onde você precisará fechar suas janelas porque começará a gritar: "NUH, ISSO É LINDIMAIS SÔ!" do fundo da sua alma e não vai parar até chegar ao índice(?) deste livro.  

Sem sombra de dúvida você já ouviu falar do incrível suporte a concorrência  e outros recursos estupendos do Clojure, mas a característica mais marcante do Clojure é que ele é um Lisp. Você explorará esse núcleo do Lisp, que é composto de duas partes: funções e dados.

### *Capítulo 4: Funções principais em profundidade*
Neste capítulo, você aprenderá sobre alguns conceitos mais aprofundados do Clojure. Isso lhe dará a base necessária para ler a documentação de funções que você ainda não terá usado e entender o que acontece quando você as experimenta.  

Você também verá exemplos de uso das funções que você vai usar mais. Isso lhe dará uma base sólida para escrever seu próprio código e para ler e aprender com os projetos de outras pessoas. E lembra que eu falei sobre perseguir vampiros purpurinados? Você fará isso neste capítulo (a menos que você já faça isso no seu tempo livre).

### *Capítulo 5: Programação Funcional*
Neste capítulo, você usará sua experiência concreta com funções e estruturas de dados e a integrará a uma nova mentalidade: a mentalidade de programação funcional. Você vai esbanjar conhecimento construindo o mais novo e mais intenso jogo que está dominando a nação: Peg Thing! (Pregador Mania(?))

### *Capítulo 6: Organizando seu projeto: Um conto de um bibliotecário*
Este capítulo explica o que são namespaces e como usá-los para organizar seu código. Não quero revelar muito, mas também envolve um ladrão de queijo internacional.

### *Capítulo 7: Alquimia do Clojure: Leitura, Avaliação e Macros*
Neste capítulo, daremos um passo para trás e descreveremos como o Clojure executa seu código. Isso lhe dará a estrutura conceitual necessária para realmente entender como o Clojure funciona e como ele é diferente de outras linguagens não Lisp. Com essa estrutura bem estabelecida, irei apresentar a macro, uma das ferramentas mais poderosas que existe!

### *Capítulo 8: Criando Macros*
Este capítulo examina detalhadamente como escrever macros, começando com exemplos básicos e avançando em complexidade. Você encerrará colocando sua cartola mágica, imaginando que administra uma loja de poções online e usando macros para validar os pedidos dos clientes.

## Parte III: Tópicos avançados
Esses capítulos abordam os tópicos super-ultra divertidos do Clojure: concorrência, interoperabilidade com Java e abstração. Embora você possa escrever programas sem entender essas ferramentas e conceitos, eles são intelectualmente recompensantes e lhe dão um poder tremendo enquanto profissional dos códigos. Um dos motivos pelo qual as pessoas dizem que aprender Clojure te faz programar melhor é o que torna os conceitos abordados nesses capítulos fáceis de entender e práticos de usar.

### *Capítulo 9:A Sagrada Arte da Programação Concorrente e Paralela*

Neste capítulo, você aprenderá o que são concorrência e paralelismo e por que eles são importantes. Você aprenderá sobre os desafios que enfrentará ao escrever programas paralelos e sobre como o design do Clojure ajuda a mitigá-los. Você usará futures, delays e promises (?) para escrever programas paralelos com segurança.

### *Capítulo 10: Metafísica do Clojure: Átomos, Refs, Vars e Zumbis do Cafuné*
Este capítulo entra em bastante detalhes sobre a abordagem do Clojure para gerenciar estado e como isso simplifica a programação concorrente. Você aprenderá como usar átomos, refs e vars, três construções para gerenciar o estado, e aprenderá como fazer computação paralela sem estado com pmap. E, sim, teremos Zumbis do Cafuné.

### *Capítulo 11: Dominando Processos Simultâneos com core.async*
Neste capítulo, você vai refletir sobre a ideia de que tudo no universo é uma máquina de self-service de cachorro-quente. Com isso, quero dizer que você aprenderá a modelar sistemas de processos de execução independente que se comunicam entre si por canais usando a biblioteca core.async.

### *Capítulo 12: Trabalhando com a JVM*
Este capítulo é como um cruzamento entre um livro de expressões e uma introdução cultural à Terra do Java. Ele fornece uma visão geral do que é a JVM, como ela executa programas e como compilar programas com ela. Ele também fornece um breve tour pelas classes e métodos Java mais usados ​​e explica como interagir com eles a partir do Clojure. Mais do que isso, ele mostra como pensar e entender Java para que você possa incorporar qualquer biblioteca Java ao seus programas em Clojure.

### *Capítulo 13: Criando e Estendendo Abstrações com Multimétodos, Protocolos e Registros(?)*
No Capítulo 4, você aprendeu que Clojure é escrito em termos de abstrações. Este capítulo serve como uma introdução ao mundo da criação e implementação de suas próprias abstrações. Você aprenderá os conceitos básicos de multimétodos, protocolos e registros(?).


### *Apêndice A: Construindo e desenvolvendo com Leiningen*
Este apêndice esclarece alguns dos pontos mais sutis do trabalho com Leiningen, como o que é Maven e como descobrir os números de versão das bibliotecas Java para que você possa utilizá-las.

### *Apêndice B: Boot, o Framework chiquérrimo para Clojure Build*
Boot é uma alternativa ao Leiningen que fornece a mesma funcionalidade, mas com o bônus adicional de que é mais fácil estender e escrever tarefas combináveis. Este apêndice explica os conceitos mais aprofundados do Boot e te orienta na escrita de suas primeiras tarefas.

# O Código
Você pode baixar todo o código-fonte do livro em http://www.nostarch.com/clojure/. O código está organizado por capítulo.

O Capítulo 1 descreve as diferentes maneiras de executar o código Clojure, incluindo como usar um REPL. Recomendo executar a maioria dos exemplos no REPL conforme você os encontrar, especialmente nos Capítulos 3 a 8. Isso te ajudará a se acostumar a escrever e entender o código Lisp, e te ajudará a reter tudo o que está aprendendo. Mas para os exemplos longos, é mais recomendável escrever seu código em um arquivo e, em seguida, executá-lo no REPL.

# A Jornada Está Começando!
Você está pronto ou pronta, valente leitor(a)? Você está pronto para encontrar seu verdadeiro destino? Pegue seu melhor par de parênteses: você está prestes a embarcar na jornada de uma vida!

Construindo, Executando e o REPL →