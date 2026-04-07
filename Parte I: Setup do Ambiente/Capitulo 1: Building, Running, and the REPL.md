*Capítulo 1* 
# Construindo, Executando e o REPL

Neste capítulo, você irá investir uma pequena quantidade de tempo se adiantando para ter familiaridade  com uma maneira rápida e infalível de construir e executar um programa em Clojure. É sensacional ter um programa de verdade rodando. Alcançar esse marco te liberta para poder experimentar, compartilhar seu trabalho e se gabar com seus colegas que ainda estão usando as linguagens da década passada. Isso irá te ajudar a se manter com motivação!

Você também irá aprender como executar código instantaneamente dentro de um processo Clojure já em execução usando o REPL (Loop de leitura-avaliação-impressão), o qual te permite testar rapidamente seu entendimento da linguagem e aprendê-la de forma mais eficaz. 

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

Este esqueleto de projeto não é inerentemente especial ou Clojuristico. É apenas uma convenção usada pelo Leiningen. Você usará Leiningen para construir e executar aplicativos Clojure, e o Leiningen espera que seu aplicativo tenha essa estrutura. O primeiro arquivo para tomar nota é o *project.clj* ➊, que é um arquivo de configuração para Leiningen. Ele ajuda o Leiningen a responder perguntas como "Quais dependências este projeto tem?" e "Quando este programa Clojure é executado, qual função deve ser executada primeiro?" Em geral, você salvará seu código-fonte em *src/<project_name>* . Neste caso, o arquivo *src/clojure_noob/core.clj* ➌ é onde você escreverá seu código Clojure, para começar. O diretório de teste ➍ obviamente contém testes, e *resources* em ➋ é onde você armazena recursos como imagens.

## Executando um projeto em Clojure


Agora vamos de fato executar o projeto. Agora abra o *src/clojure_noob/core.clj* no seu editor favorito. Você deve ver isso:

```
➊ (ns clojure-noob.core
  (:gen-class))

➋ (defn -main
  "Eu não faço quase nada..."
  [& args]
➌   (println "Hello, World!"))

```
As linhas no ➊ declaram o namespace. Na qual você não precisa se preocupar agora. A função main ➋ é o ponto de entrada do seu programa, um tópico que sera abordado no Apêndice A. Por agora troque o texto ```"Hello, World!"``` do ➌ por ```"Sou uma chaleirinha"```. A linha inteira ```(println "Sou uma chaleirinha")```.

Em seguida, navegue para o diretório clojure.noob no seu terminal e dê enter:

```lein run```

E você deverá ver a saída **"Sou uma chaleirinha"** .
Parabéns, Chaleirinha. Você escreveu e executou o programa.

Você aprenderá mais sobre o que de fato aconteceu agora no programa de acordo com o que você for lendo o livro. Mas por agora, tudo que você precisa saber e que você criou uma função ```-main``` e essa função executou quando você digitou o comando lein run no terminal. 

## Construindo um projeto Clojure

Usar lein run é ótimo para testar coisas, mas e se você quiser compartilhar seu trabalho com pessoas que não tem o Leiningen instalado?  Para fazer isso você pode criar um arquivo independente que qualquer pessoa com Java instalado (que basicamente todo mundo tem) consegue executar. Para criar esse arquivo execute isto:

``` lein uberjar``` 

Esse comando cria o arquivo *target/uberjar/clojure-noob-0.1.0-SNAPSHOT-standalone.jar.* e você pode fazer o Java executa-lo ao rodar isso:
 ``` java -jar target/uberjar/clojure-noob-0.10-SNAPSHOT-standalone.jar ```

Veja isso! O arquivo *target/uberjar/clojure-noob-0.1.0-SNAPSHOT-standalone.jar.* é o seu novo e premiado programa Clojure o qual você consegue distribuir e rodar em quase qualquer plataforma. 

basicamente agora você tem  todos as informações para construir, executar e distribuir programas clojures (bem) básicos.

Nos próximos capitulos você aprenderá mais sobre o que o Lein está fazendo enquanto você executou os comandos anteriores, ganhando um entendimento completo da relação do Clojure com a JVM e como você pode executar códigos em produção.

Antes de você ir para o capitulo 2 e discutir as glorias e as maravilhas do Emacs vamos a outra importante ferramenta: o REPL.

## Usando o REPL

O REPL é uma ferramenta para experimentar o código. Ele te permite interagir com um programa em execução e rapidamente testar ideas. Ele faz isso ao te disponibilizar um prompt para execução de código. Ele lê seu input, o avalia, imprime o resultado e faz um loop disponibilizando o prompt novamente.

Esse processo permite um ciclo de feedback rápido que não seria possível na maioria das outras linguagens. Eu fortemente recomendo que você use o REPL com frequência, porque você sera capaz de checar seu entendimento do Clojure enquanto você aprende. Além disso o desenvolvimento usando o REPL é uma parte essencial da experiencia Clojure, e você estaria perdendo muito se não usa-lo. 

Para iniciar o REPL execute isso

``` lein repl```

A saída (? ver padronização) deverá ser parecer com isso:

``` 
nREPL server started on port 28925
REPL-y 0.1.10
Clojure 1.9.0
    Exit: Control+D or (exit) or (quit)
Commands: (user/help)
    Docs: (doc nome-da-função-aqui)
          (find-doc "parte-do-nome-aqui")
  Source: (source nome-da-função-aqui)
          (user/magia nome-da-função-aqui)
 Javadoc: (javadoc java-object-ou-classe-aqui)
Examples from clojuredocs.org: [clojuredocs or cdoc]
          (user/clojuredocs nome-aqui)
          (user/clojuredocs "ns-aqui" "nome-aqui")
clojure-noob.core=>

```

A ultima linha ``` clojure-noob.core=>``` , te diz que você está no namespace clojure-noob.core. você aprender sobre namespaces depois, mas note que o namespace basicamente corresponde o arquivo src/clojure_noob/core/clj também note que o REPL mostra a versão do Clojure 1.9.0 mas como mencionado antes tudo funcioará normalmente independentemente da versão que você usar. 

O prompt também indica que seu código está carregado no REPL, e você pode executar as funcoes que foram definidas. Por agora so temos uma função ```-main``` definida. Vá em frente e execute isso:

```
clojure-noob.core=> (-main)
"Sou uma chaleirinha"
nil
```

Bom trabalho! você acabou de usar o REPL para avaliar a chamada da função -main.
Tente algumas outras funcoes básicas de Clojure:

```
clojure-noob.core=> (+ 1 2 3 4)
10
clojure-noob.core=> (* 1 2 3 4)
24
clojure-noob.core=> (first [1 2 3 4])
1
```

Incrível! você somou alguns números, multiplicou alguns números e pegou o primeiro elemento de um vetor. você também teve seu primeiro encontro com a estranha sintaxe de Lisp! Todos os Lisps, incluindo o Clojure, empregam a notação de prefixo, isto significa que o operador sempre vem primeiro em uma expressão. Se você tem duvida do que isso significa, não se preocupe, você aprenderá sobre a sintaxe do Clojure logo mais. 

Conceitualmente o REPL é similar a um SSH (Secure Shell). Da mesma maneira que você pode usar o SSH para interagir com um servidor remoto o REPL do Clojure permite que você interaja com o processo do Clojure em execução. Esta funcionalidade é bastante poderosa porque você pode ate mesmo anexar em REPL a um aplicativo ativo em produção, e modificar seu programa enquanto ele esta sendo executado. Por agora você usara o REPL para para construir seu conhecimento da sintaxe e da semântica do Clojure. 

Mais uma coisa: mais pra frente este livro apresentara códigos sem prompt do REPL, mas por favor sempre experimente executar o código. Segue um exemplo:

```
(do (println "sem prompt aqui!")
   (+ 1 3))
; => sem prompt aqui!
; => 4
```

Quando você ver um trecho de código como este , as linhas que começam com ;=> indicam que o output do código que esta sendo executado. Neste caso, a frase ```sem prompt aqui``` deve ser exibida e o valor de retorno do código é 4. 

## Editores de Clojure

A essa altura você devera ter o conhecimento básico que você precisa para aprender Clojure sem ter que se meter com um editor ou IDE (integrated development environment - ambiente de desenvolvimento integrado). Mas se você de fato quiser um bom tutorial de um poderoso editor, o capitulo cobre Emacs, o editor mais popular entre os Clojuristas. você absolutamente não precisa usar Emacs para desenvolvimento em Clojure, mas o Emacs oferece uma integração muito boa com o REPL do Clojure e é muito adequado para escrever códigos Lisp. O que é mais importante, porem, é usar o que funcionar para você.

Se Emacs não for sua praia, seguem alguns materiais sobre editores e IDEs para desenvolver Clojure:

- Esse video do YouTube te mostrara como configurar o Sublime Text 2 para o desenvolvimento  em Clojure: http://www.youtube.com/watch?v=wBl0rYXQdGg/.
- Vim tem boas ferramentas para o desenvolvimento  em Clojure. Este artigo é um bom começo: http://mybuddymichael.com/writings/writing-clojure-with-vim-in-2013.html.
- Counterclockwise é um plugin altamente recomendado para Eclipse: https://github.com/laurentpetit/ccw/wiki/GoogleCodeHome.
- Cursive Clojure é a IDE recomendada para quem usa IntelliJ: https://cursiveclojure.com/
- Nightcode é uma IDE simples e gratuita escrita em Clojure: https://github.com/oakes/Nightcode/.

(?) biscoito para nosso colega BR ? (definir se autor autoriza)
https://plugins.jetbrains.com/plugin/22489-clojure-lsp 


## Summary

Estou muito orgulhoso de você, querida Chaleirinha. você executou o seu primeiro programa Clojure! não apenas, você começou a se familiarizar com o REPL, uma das ferramentas mais importantes para desenvolver programas Clojure. Incrível, isto me faz lembrar dos versos imortais de *Long Live* (Vida Longa), de umas das minhas heroínas pessoais preferidas:


You held your head like a hero - Você manteve sua cabeça erguida como um herói
On a history book page         - em um pagina de um livro de historia    
It was the end of a decade     - esse foi o fim de uma década  
But the start of an age        - mas o inicio de uma era.  
                         —Taylor Swift

Bravo!