*Capítulo 1* 
# Construindo, Executando e o REPL

Neste capítulo, você irá investir uma pequena quantidade de tempo se adiantando para ter familiaridade  com uma maneira rápida e infalível de construir e executar um programa em Clojure. É sensacional ter um programa de verdade rodando. Alcançar esse marco te liberta para poder experimentar, compartilhar seu trabalho e se gabar com seus colegas que ainda estão usando as linguagens da década passada. Isso irá te ajudar a se manter com motivação!

Você também irá aprender como executar código instantaneamente dentro de um processo Clojure já em execução usindo o REPL (Loop de leitura-avaliação-impressão), o qual te permite testar rapidamente seu entendimento da linguagem e aprendê-la de forma mais eficaz. 

Mas primeiro, irei rapidamente te apresentar ao Clojure. Na sequência, abordarei Leiningen, a ferramenta padrão de fato(?) para de construção para Clojure. Ao final do capítulo, você saberá como fazer o seguinte:

- Criar um novo projeto Clojure com Leiningen
- Construir o projeto para criar um arquivo JAR executável
- Executar o arquivo JAR
- Executar o código Clojure em um REPL

## Primeiro as coisas mais importantes: o que é Clojure?

Clojure foi forjado em um vulcão mítico por Rich Hickey. Usando uma liga de Lisp, programação funcional e uma mecha de seu próprio, iradíssimo, cabelo, ele criou uma linguagem que é encantadora, mas  também poderosa. Sua ascendência Lisp lhe dá o poder de escrevermos código de forma mais expressiva do que é possível na maioria das linguagens não Lisp, e sua abordagem diferenciada na programação funcional deixará seu pensamento como pessoa programadora mais aguçado. Além disso, Clojure te fornece melhores ferramentas para lidar com domínios complexos (como programação concorrente), que são tradicionalmente conhecidos por levar os desenvolvedores a anos de terapia.

Ao falar sobre Clojure é importante ter em mente a diferença entre a linguagem Clojure e o compilador Clojure. A linguagem Clojure é um dialeto Lisp com ênfase funcional cuja sintaxe e semântica são independentes de qualquer implementação. O compilador é um arquivo JAR executável, *clojure.jar*, que pega o código escrito na linguagem Clojure e o compila para o bytecode da JVM (Java Virtual Machine -  Máquina Virtual do Java). Você verá Clojure sendo usado para se referir à linguagem e ao compilador, o que pode ser confuso se você não estiver ciente de que são coisas separadas. Mas agora que você está ciente, tudo vai ficar bem.

Essa distinção é necessária porque, diferentemente da maioria das linguagens de programação como Ruby, Python, C e um zilhão de outras, Clojure é uma *linguagem hospedada*. Os programas Clojure são executados dentro da JVM e dependem da JVM para recursos essenciais como threading e coleta de lixo(?). Clojure também pode ser executado para o JavaScript e o Microsoft Common Language Runtime (CLR), mas este livro foca apenas na implementação da JVM.

Exploraremos a relação entre Clojure e a JVM mais adiante, mas por enquanto os principais conceitos que você precisa entender são:

- Os processos JVM executam bytecode Java
- Normalmente, o compilador Java produz bytecode Java a partir do código-fonte Java.
- Os arquivos JAR são coleções de bytecode Java.
- Os programas Java geralmente são distribuídos como arquivos JAR.
- O programa Java *clojure.jar* lê o código-fonte Clojure e produz bytecode Java.
- Esse bytecode Java é então executado pelo mesmo processo JVM que já está executando /*clojure.jar*.

O Clojure continua evoluindo. No momento em que este texto foi escrito, ele estava na versão 1.9.0, e o desenvolvimento está indo de vento em popa. Se você estiver lendo este livro em um futuro distante e Clojure tiver um número de versão maior, não se preocupe! Este livro aborda os fundamentos do Clojure, que não devem mudar de uma versão para a outra. Não há necessidade de seu mordomo robô devolver este livro à livraria.

Agora que você sabe o que é o Clojure, vamos realmente um puxa(?) programa em Clojure!

# Leiningen

Nos dias de hoje a maioria dos Clojuristas usa Leiningen para construir e gerenciar seus projetos. Você pode ler uma descrição completa de Leiningen no Apêndice A, mas por enquanto vamos nos concentrar em usá-lo para quatro tarefas:

1. Criar um novo projeto Clojure
2. Executar o projeto Clojure
3. Construir o projeto Clojure
4. Usar o REPL

Antes de continuar, certifique-se de ter instalado o Java versão 1.6 ou posterior. Você pode verificar sua versão executando `java -version` em seu terminal, e baixar o Java Runtime Environment (JRE)(?) mais recente em http://www.oracle.com/technetwork/java/javase/downloads/index.html. 
Em seguida, instale o Leiningen usando as instruções na página inicial do Leiningen em http://leiningen.org/ (usuários do Windows, observem que há um instalador específico para Windows). Quando você instala o Leiningen, ele baixa automaticamente o compilador Clojure, *clojure.jar*.

## Criando um novo projeto Clojure

Criar um novo projeto Clojure é muito simples. Um único comando Leiningen cria um esqueleto do projeto. Mais tarde, você aprenderá como fazer tarefas tipo incorporar bibliotecas Clojure, mas por enquanto, essas instruções permitirão que você execute o código que você escreve.

Vá em frente e crie seu primeiro projeto Clojure digitando o seguinte em seu terminal:

```lein new app clojure-noob```

Este comando deverá criar uma estrutura de pastas semelhante a esta (não tem problema se houver algumas diferenças):

| .gitignore
| doc
| | intro.md
➊ | project.clj
| README.md
➋ | resources
| src
| | clojure_noob
➌ | | | core.clj
➍ | test
| | clojure_noob
| | | core_test.clj

Este esqueleto de projeto não é inerentemente especial ou Clojuristico. É apenas uma convenção usada pelo Leiningen. Você usará Leiningen para construir e executar aplicativos Clojure, e o Leiningen espera que seu aplicativo tenha essa estrutura. O primeiro arquivo para tomar nota é o *project.clj* ➊, que é um arquivo de configuração para Leiningen. Ele ajuda o Leiningen a responder perguntas como "Quais dependências este projeto tem?" e "Quando este programa Clojure é executado, qual função deve ser executada primeiro?" Em geral, você salvará seu código-fonte em *src/<project_name>* . Neste caso, o arquivo *src/clojure_noob/core.clj* ➌ é onde você escreverá seu código Clojure, para começar. O diretório de teste ➍ obviamente contém testes, e *resources* em ➋ é onde você armazena recursos como imagens, por exemplo.


