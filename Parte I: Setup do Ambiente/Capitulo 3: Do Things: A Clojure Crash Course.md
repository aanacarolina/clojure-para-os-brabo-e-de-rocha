### *Capítulo 3: Faça coisas: Curso intensivo de Clojure*

Chegou a hora de aprender como de fato *fazer coisas* com Clojure! Caramba!
Apesar de você, sem sombra de dúvidas já ter ouvido do incrível suporte do Clojure a concorrencia e outras estupendas funcionalidade, a caracteristicas mais aparentes é que ele é um LISP. Neste capítulo, você vai explorar os elementos centrais que compoem este Lisp: sintaxe, funções e dados.
Juntos eles irão te dar uma fundação sólida para representar e resolver problemas em Clojure.

Após definirmos este trabalho de base você será capaz de escrever algum código super importantes. Na última sessão você irá amarrar tudo junto ao criar o modelo de Hobbit, e escrever uma função para atingir ele num lugar aleatório. Super! Importante!

Conforme você for passando por este capítulo, eu recomendo que você digite os exemplos num REPL e os execute. Programar numa nova linguagem é uma habilidade e assim como Iodelei ou nado sincronizado, você precisa praticar para aprender. A proposito nado sincronizado para iodeleiros brabos e de rocha será publicado em Agosto de 2000 e nunca. Fiquem de olho.

## Sintaxe

A sintaxe do Clojure é simples. Como todos os Lisps ele utiliza uma estrutura uniforme, um punhado de operadores especiais e um fornecimento constante de parenteses entregues pela mina de parenteses escondidas embaixo do Massachusetts Institute of Technology, onde o Lisp nasceu.

# Formas

Todo o código clojure é escrito numa estrutura uniforme. O Clojure reconhece dois tipos de estruturas:

- Representações literais de estrutura de dados (como números, strings, mapas e vetores)
- Operações

Nós usamos o termo *form* para se referir a um código válido. Eu irei usar *expression* para se referir a uma form do Clojure, mas não se apegue muito a terminologia. O Clojure *avalia* cada form para produzir um valor. Estas representações literais são todas formas válidas:

```clojure 
1 
"a string" 
["a" "vector" "of" "strings"] 
```

O teu código raramente irá ter valores literais boiando soltos, pois obviamente, eles não fazem nada sozinhos. Ao invés disso, você irá usar valores literais em operações. Operações são como você *faz coisas*. Todas as operações têm essa forma *Abre parentes, operador, operandos, fecha parentes* :

```clojure
(operator operand1 operand2 ... operandn)
```
Perceba que não tem virgulas. O Clojure usa espaços para separar operandos e trata virgulas como se fossem espacos em branco. Seguem algumas operações de exemplo:

```clojure
(+ 1 2 3)
; => 6

(str "It was the panda " "in the library " "with a dust buster")
; => "It was the panda in the library with a dust buster"
```

Na primeira operação, o operador _*_ soma os operandos *1*, *2* e *3*. Na segunda operação, o operador *str* concatena três _strings_ para formar uma nova _string_. Ambas formas são válidas. Segue ai algo que não é uma forma porque nao tem um parenteses sendo fechado.

```clojure
(+
```

A uniformidade estrutural do Clojure é provavelmente diferente do que você deve ter se acostumado. Em outras linguagens diferentes operações podem ter estruturas diferentes dependendo do operador e dos operandos. Por exemplo, o Javascript utiliza um rodízio de pizzas de notações fixas, operadores de ponto e parenteses:

```javascript
1 + 2 + 3
"It was the panda ".concat("in the library ", "with a dust buster")
```

A estrutura do Clojure é muito simples e consistente em comparação. Nao interessa qual operador voce estiver usando ou o tipo de dados no qual voce estiver operando, a estrutura permanece a mesma.

## Fluxo de Controle

Vamos dar uma olhada em três controles de fluxo basicos: *if*, *do* e *when*.
Ao longo do livro você encotrará mais outros, mas esses vão dar um gostinho:

# if
Essa é uma estrutura geral para uma expressão usando *if*:
```clojure
(if boolean-form
  then-form
  optional-else-form)
```

(?) revisar se traduzir o codigo

Uma forma Booleana é apenas uma forma que é avaliada para um valor 
verdadeiro ou falso. Você irá aprender sobre veracidade ou falsidade na próxima seção. Segue mais um par de exemplos de *if*:

```clojure
(if true
  "Pelo martelo de Zeus!"
"Pelo tridente do Aquaman!")
; => "Pelo martelo de Zeus!"

(if false
  "Pelo martelo de Zeus!"
"Pelo tridente do Aquaman!")
; => "Pelo tridente do Aquaman!"
```
(?)

O primeiro exemplo retorna `Pelo martelo de Zeus` porque a forma Booleana é avaliada como `true`, um valor verdadeiro, e o segundo exemplo retorna `Pelo tridente do Aquaman!`porque a forma Booleana é `false`, avaliada como um valor falso.

Você também pode omitir o bloco do `else`. Se você fizer isso e a expressão Booleana for falsa, o Clojure retorna `nil`, dessa forma:

```clojure
(if false
  "Pelo cotovelo de Odin!")
; => nil
```

Repare que `if` usa a posição do operando para associar operandos com os blocos `then` e `else`: o primeiro operando é o bloco `then` e o segundo operando é o bloco (opcional) `else`. Como resultado, cada bloco somente possui uma forma. Isso é diferente da maioria das linguagens. Por exemplo, em Ruby você pode escrever o seguinte:


```clojure
if true
  doer.do_thing(1)
  doer.do_thing(2)
else
  other_doer.do_thing(1)
  other_doer.do_thing(2)
end
```

Para contarnar esse aparente limitação podemos usar o operador `do`.

# do
O operador `do` nos deixa _envelopar_ multiplas formas nos parenteses e executar cada uma delas. Tente o seguinte no seu REPL:

```clojure
(if true
  (do (println "Sucesso total!")
      "Pelo martelo de Zeus!")
  (do (println "Errou!")
      "Pelo tridente do Aquaman!"))
; => Sucesso total!
; =>  "Pelo martelo de Zeus!"
```

Este operador te permite fazer várias coisas em cada expressão do bloco `if`. Nesse caso, duas coisas acontecem:
`Sucesso total!` é impresso no REPL e  `"Pelo martelo de Zeus!"` é o valor de retorno da expressão `if` inteira.

# when

O operador `when` é como se fosse uma combinação do `if` e `do`, mas sem o bloco do `else`. Segue um exemplo:

```clojure
(when true
  (println "Sucesso total!")
  "abra cadabra")
; => Sucesso total!
; => "abra cadabra"
```

Use o `when` se voce quiser fazer multiplas coisas quando uma condição for verdadeira, e sempre quiser retornar `nil` quando a condição for falsa.

# nil, true, false, veracidade, iqualidade e expressoes Booleanas

O Clojure tem o valores `true` e `falso`. No Clojure o `nil` é usado para indicar _nenhum valor_ . Você pode verificar se um valor é `nil` com a função apropriadamente chamada de `nil?`:

```clojure
(nil? 1)
; => false

(nil? nil)
; => true
```

Ambos `nil` e `false` são usados para representar falsidade lógica, sendo todos os outros valores logicamente verdadeiros. _Truthy_ e _Falsey_ se referem a como um valor é tratado em uma expressão Booleana, como na primeira expressão que passamos pro `if`:

```clojure
(if "ursos comem beterraba"
"ursos beterrabam Battlestar Galactica")
; => "ursos beterrabam Battlestar Galactica"

(if nil 
  "Esse não será o resultado porque nil é falsey"
  "nil é falsey")
; => "nil é falsey"
```

No primeiro exemplo, a string `ursos comem beterraba` é considerada _truthy_, então a expressão é avaliada pra `ursos beterrabam Battlestar Galactica`. O segundo exemplo mostra um valor _falsey_ sendo _falsey_.

O operador de igualidade do Clojure é `=`:

```clojure
(= 1 1)
; => true

(= nil nil)
; => true

(= 1 2)
; => false
```

Algumas outras linguagens exigem que você utilize diferentes operadores ao comparar valores de diferentes tipos. Por exemplo, talvez você tenha que usar algum tipo especial de operador de igualdade de string, feito especialmente para strings. Mas você nao precisa de nada estranho ou tedioso do tipo para testar a igualdade ao usar as estruturas de dados built-in do Clojure. 

O Clojure usa os operadores Booleanos `or` e `and`. O `or` retorna ou o primeiro valor verdadeiro ou o último valor. O `and` retorna o primeiro valor falso ou, se nenhum valor for falso, o último valor verdadeiro. Vamos ver o `or` primeiro:

```clojure
(or false nil :grande_quero_dizer_venti :por_que_nao_posso_dizer_grande)
; => :grande_quero_dizer_venti

(or (= 0 1) (= "sim" "não"))
; => false

(or nil)
; => nil
```

No primeiro exemplo o valor do retorno é `:grande_quero_dizer_venti` porque este é o primeiro valor verdadeiro. O segundo exemplo não possui valor verdadeiro, entao o `or` retorna o ultimo valor, o qual é `false`. No ultimo exemplo, novamente nao existe valor verdadeiro, e o `or` retorna o ultimo valor, o qual é `nil`.  E agora vamos ver o `and`:

```clojure
(and :wifi_gratis :cafe_quentinho)
; => :cafe_quentinho

(and :de_boa_na_lagoa nil false)
; => nil
```

No primeiro exemplo o `and` retorna o ultimo valor verdadeiro `:cafe_quentinho` No segundo exemplo, `and` retorna `nil`, o qual é o primeiro valor falso. 

## Nomeando valores com def

No Clojure você usa `def` para vincular (`bind`)um nome a um valor 

```clojure
(def nomes-errados-de-protagonistas
  ["Larry Potter" "Dorinha a aventureira" "O Incrivel Bulk"])

nomes-errados-de-protagonistas
; => ["Larry Potter" "Dorinha a aventureira" "O Incrivel Bulk"]

```

Neste caso voce está associando o nome `nomes-errados-de-protagonistas` com um vetor contendo três coisas (você irá aprender sobre vetores em [Vetores na pagina 45](?) TODO add link)).

Note que eu estou usando o termo vincular, onde em outras linguagens você diria que voce está atribuindo (_assigning_) um valor para uma _variável_. Outras linguagens te encorajam a performar multiplas atribuicoes para a mesma variavel.

Por exemplo, em Ruby voce precisa performar varias atribuicoes para uma variavel para estabelecer o seu valor.


```ruby
severidade = :moderada
mensagem_de_erro = "MEU DEUS! É UM DESASTRE, NÓS ESTAMOS..."
if severidade == :moderada
messagem_de_erro = messagem_de_erro + "MODERADAMENTE INCONVENIENTES"
else
mensagem_de_erro = mensagem_de_erro + "LASCADOS!"
end
```

Você deve estar tentando a fazer algo similar em Clojure:

```clojure
(def severidade :moderada)
(def mensagem_de_erro "MEU DEUS! É UM DESASTRE, NÓS ESTAMOS ")
(if (= severidade :moderada)
    (def messagem_de_erro (str messagem_de_erro + "MODERADAMENTE INCOMODADOS"))
    (def mensagem_de_erro (str mensagem_de_erro + "LASCADOS!")))
```

Entretanto alterar o valor associado com um nome como este pode dificultar a compreensao do comportamento do seu programa, porque é mais dificil de entender qual valor está associado a um nome ou porque aquele valor tenha sido alterado. O Clojure tem um conjunto de ferramentas para lidar com mudanças, o qual voce ira aprender sobre no capítulo 10. Enquanto voce estiver aprendendo Clojure, voce descobrirá que voce raramente precisa alterar um nome/valor associado. Segue uma maneira de como poderia escrever o codigo anterior:


```clojure
(defn mensagem_de_erro
  [severidade]
  (str "MEU DEUS! É UM DESASTRE, NÓS ESTAMOS "
       (if (= severidade :moderada)
         "MODERADAMENTE INCOMODADOS"
         "LASCADOS!")))

(mensagem_de_erro :moderada)
; => "MEU DEUS! É UM DESASTRE, NÓS ESTAMOS MODERADAMENTE INCOMODADOS!"
```

Aqui, voce criou uma funcao `mensagem_de_erro`, a qual aceita um unico argumento, `severidade`, e o utiliza para determinar qual string retornará. Vocé, entao, chama a funcao com `moderada` para a severidade. Voce ira aprender tudo sobre criacao de funcao em [functions na pagina 48](?) TODO add link; enquanto isso, voce deve tratar `def` como se tivesse definindo uma constante. Nos proximos capitulos, voce ira aprender como trabalhar com esta, aparente, limitacao ao adotar o paradigma da programacao funcional. 

# Estrutura de Dados

O Clojure vem com um punhado de estrutura de dados que voce usará na maior parte do tempo. Se voce estiver vindo de uma experiencia de Orientação a Objetos, você ficará surpresa com o quanto voce pode fazer com os tipos, aparentemente, básicos apresentados aqui.
Todas as estruturas de dados do Clojure são imutáveis, ou seja, não é possível alterá-las diretamente. Por exemplo, em Ruby voce pode reatribuir o nome errado dos protagonistas na posição(?) 0:

``` ruby
nomes_errados_de_protagonistas = [
  "Larry Potter", 
  "Dorinha a aventureira", 
  "O Incrivel Bulk"
  ]

nomes_errados_de_protagonistas[0] = "Gary Potter"

nomes_errados_de_protagonistas
# => [
#   "Gary Potter",
#   "Dorinha a aventureira",
#   "O Incrivel Bulk"
# ]
```

O Clojure nao tem um equivalente a isso. Voce aprendera mais sobre o porque o Clojure foi implementado dessa forma no Capitulo 10, mas por enquanto é mais divertido aprender sem todas essas filosofias. Sem mais delongas, vamos ver numeros em Clojure.

# Números

O Clojure tem um suporte para numeros bastante sofisticado. Eu não irei perder muito ficando nesses detalhes tecnicos chatos (como coesão e contágio numérico), porque isso vai nos atrapalhar a fazer as coisas. Se voce tem interesse nesses detalhes chatos, confira a documentação em [https://clojure.org/reference/data_structures#Numbers](https://clojure.org/reference/data_structures#Numbers). Resumindo, o Clojure lida de boa com praticamente qualquer coisa que você jogar pra ele.

Enquanto isso iremos trabalhar com inteiros e casas decimais. Nos tambem iremos trabalhar com frações, no qual o clojure pode representar diretamente. Aqui estão um inteiro, um numero com casas decimais e uma fração, respectivamente:

``` clojure
93
1.2
1/5
``` 

# Strings

Strings representam texto!. O nome vem dos antigos Fenícios, que um dia inventaram o alfabeto por conta de um acidente envolvendo um novelo. _(string em inglês significa fio)_ Seguem alguns exemplos de strings literais:

``` clojure
"Lord Voldemort"
"\"Aquele que não pode ser nomeado\""
"\"Grande vaca de Moscou!\" - Hermes Conrad"
```

Perceba que o Clojure somente permite aspas duplas para delinear strings. 'Lord Voldemort', por exemplo, não é uma string válida. Perceba também que o Clojure não tem interpolação de strings. Ele somente permite concatenação através da função 'str'.

``` clojure

(def nome "Chewbacca")
(str "\"Uggllglglglglglglglll\" - " nome)
; => "Uggllglglglglglglglll" - Chewbacca
```

[Ilustração em preto e branco de um Wookiee, personagem da série Star Wars, com o punho levantado e uma expressão facial feroz. Um balão de fala acima da cabeça exibe o som "Uggllglglglglgl".](wookie.png)

# Mapas

Mapas são semelhantes a dicionários ou hashes em outras linguages. Eles são uma maneira de associar algum valor com outro valor. Os dois tipos de mapas em Clojure são hash maps e sorted maps (mapas ordenados). Irei cobrir apenas o mais basico hash maps. Vamos dar uma olhada em alguns exemplos de mapas literais. Aqui está um mapa vazio:

``` clojure
{}
``` 

Neste exemplo, :nome e :sobrenome são keywords (falarei sobre elas na proxima seção):

``` clojure
{:nome "Carlos"
 :sobrenome "McPeixe"}
 ```

Aqui nós associamos a "chave-string" com a função '+' :

{"chave-string" +}

Mapas podem ser aninhados:

``` clojure
{:nome {:primeiro "João" :meio "Jacó" :ultimo "daSilvaSantos"}}
```

Perceba que os valores do mapa podem ser de qualquer tipo: strings, numeros, mapas, vetores e até funções. O Clojure não liga!

Além de usar mapas literais, também podemos usar a função hash-map para criar um mapa:

``` clojure
(hash-map :a 1 :b 2)
; => {:a 1 :b 2}
```

Você pode procurar valores em mapas com a função 'get':

``` clojure
(get {:a 0 :b 1} :b)
; => 1

(get {:a 0 :b {:c "uh hum"}} :b)
; => {:c "uh hum"}
```

Em ambos os exemplos, nós pedimos para o 'get' o valor da chave :b no mapa - no primeiro caso ele retorna 1 e no segundo caso ele retorna o mapa aninhado '{:c "uh hum"}'

'get' irá retornar 'nil' se ele não encontrar a sua chave ou você pode passar um valor de retorno padrão, tipo : "unicórnios?".

``` clojure
(get {:a 0 :b 1} :c)
; => nil

(get {:a 0 :b 1} :c "unicórnios?")
; => "unicórnios?"
```

A função get-in te permite procurar valores em mapas aninhados:

``` clojure
(get-in {:a 0 :b {:c "uh hum"}} [:b :c])
; => "uh hum"
```

Um outro jeito de procurar um valor em um mapa é tratar o mapa como uma função, usando a chave como seu argumento:

``` clojure
({:nome "O bule humano"} :nome)
; => "O bule humano"
```

Outra coisa legal que você pode fazer com mapas é usar keywords como funções para procurar valores, o que nos leva ao nosso próximo assunto, keywords (palavras-chave).

# Keywords 

Para entender melhor as keywords em Clojure é melhor vermos como elas sao usadas. Elas são usadas primariamente em mapas, como voce viu na seção anterior. Seguem alguns exemplos de keywords:

``` clojure
:a
:rumplestiltsken
:34
:_?
``` 

As keywords podem ser usadas como funções que procuram o valor correspondente em uma estrutura de dados. Por exemplo, voce pode procurar `:a` em um mapa:

``` clojure
(:a {:a 1 :b 2 :c 3})
; => 1
```

Isso equivale a 

``` clojure
(get {:a 1 :b 2 :c 3} :a)
; => 1
```

Você pode passar uma valor padrão, usando o `get`:

``` clojure
(:d {:a 1 :b 2 :c 3} "Nenhum gnomo conhece as casas, como o gnomo de jardim Noe")
; => "Nenhum gnomo conhece as casas, como o gnomo de jardim Noe"
```

Usar uma keyword como função é prazerosamente sucinto e Clojuristas Reais o fazem sempre. Você deveria fazer também!

# Vetores

Um vetor é parecido com uma matriz, no sentido que é uma collection que começa com indice 0. Por exemplo, segue um vetor literal:

``` clojure
[3 2 1]
```

E aqui retornamos o elemento na posicao 0 de um vetor:

``` clojure
(get [3 2 1] 0)
; => 3
```

Segue outro exemplo de get pelo posição:

``` clojure
(get ["a" {:nome "Pugsley Winterbottom"} "c"] 1)
; => {:nome "Pugsley Winterbottom"}
```

Veja que os elementos de um vetor podem ser de qualquer tipo, e voce pode misturar os tipos. Perceba também que estamos usando a mesma funcao `get` como usamos quando estávamos procurando valores em mapas:

Voce pode criar vetores com a função `vector`:

``` clojure
(vector "arrepiante" "lua" "cheia")
; => ["arrepiante" "lua" "cheia"]
```

Você pode usar a função `conj` para incluir elementos adicionais no vetor. Esses elementos são adicionados no `final` de um vetor:

``` clojure
(conj [1 2 3] 4)
; => [1 2 3 4]
```

Vetores não sao o unico jeito de guardar sequencias; o Clojure também tem listas.

# Listas

Listas são parecidas com vetores, no sentido que elas sao colecoes lineares e valores. Mas tem suas diferencas. Por exemplo, voce nao consegue buscar elementos de uma lista com `get`. Para escrever uma lista literal, basta inserir os elementos entre parenteses e usar aspas simples no começo

``` clojure
'(1 2 3 4)
; => (1 2 3 4)
```

Perceba que quando o REPL imprime a lista, ele nao inclui as aspas simples. Nós voltaremos para explicar porque isso acontece no Capitulo 7. Se voce quiser buscar um elemento de uma lista, voce pode usar a funcao `nth`:


``` clojure
(nth '(:a :b :c) 0)
; => :a

(nth '(:a :b :c) 2)
; => :c
```

Eu não vou cobrir performance em detalhe nesse livro porque eu nao acho que seja util focar nisso até a linguagem se tornar familiar para você. De todo modo, é bom saber que usar `nth` para buscar um elemento de uma lista é mais lento que usar `get` para buscar um elemento de um vetor. Isso se dá porque o Clojure tem que atravessar todos os _n_ elementos de uma lista para achar o _enésimo_  (nth), enquanto que para acessar um elemento de um vetor pelo seu indice bastam algums poucos pulos, na maioria dos casos.

Valores em uma lista poder ser de diferentes tipos e voce pode criar listas com a função `list`:

``` clojure
(list 1 "two" {3 4})
; => (1 "two" {3 4})
```

Os elementos são adicionados no _começo_ de uma lista:

``` clojure
(conj '(1 2 3) 4)
; => (4 1 2 3)
```

Quando voce deve usar uma lista e quando deve usar um vetor? Uma boa regra geral é que se voce precisa adicionar itens facilmente no inicio de uma sequencia ou se voce estiver escrevendo uma macro, voce deverá usar uma lista. Do contrario, use um vetor. De acordo com que voce for aprendendo mais, voce vai comecar a ter uma boa nocao de quando usar qual.

# Conjuntos 

Conjuntos são collections de valores únicos. O Clojure tem dois tipos de conjuntos: hash e ordenados. Irei focar nos conjuntos hash (hash set) pois eles são usados com mais frequencia. Segue a notação literal de um conjunto hash:

``` clojure
#{"kurt vonnegut" 20 :icicle}
```

Você também pode criar um conjunto usando a função hash-set:
``` clojure
(hash-set 1 1 2 2)
; => #{1 2}
```

Perceba que multiplas instâncias de um valor se torna um unico valor no conjunto, então ficamos com um unico 1 e um unico 2. Se voce tentar adicionar um valor em um conjunto que ja possui aquele valor (como :b no codigo abaixo), ainda assim o conjunto terá apenas um unico elemento desse valor:

``` clojure
(conj #{:a :b} :b)
; => #{:a :b}
```

Você também pode criar conjuntos a partir de vetores e listas existentes usando a função _set_:

``` clojure
(set [3 3 3 4 4])
; => #{3 4}
```

Você pode verificar se um valor pertence a um conjunto usando a função _constains?_, _get_ ou usando uma keyword como função, usando o conjunto como seu argumento. A função _contains?_ retorna true ou false, enquanro que _get_ e buscar por keyword irão retornar o valor, caso exista, ou do contrário, nil. 

Veja como usar _contains?_:

``` clojure
(contains? #{:a :b} :a)
; => true

(contains? #{:a :b} 3)
; => false

(contains? #{nil} nil)
; => true
```

Veja como usar uma keyword:

``` clojure
(:a #{:a :b})
; => :a
```

Veja como usar _get_:

``` clojure
(get #{:a :b} :a)
; => :a

(get #{:a nil} nil)
; => nil

(get #{:a :b} "kurt vonnegut")
; => nil
```

Perceba que ao usar _get_ para testar se um conjunto contem ou não _nil_ irá sempre retornar _nil_, o que é confuso. A função _contains?_ pode ser a melhor opção quando você estiver testando especificamente para pertencimento. 

# Simplicity

Você deve ter percebido que o tratamento das estruturas de dados até o momento não incluem a descrição de como criar novos tipos ou classes. O motivo é que a enfase do Clojure em simplicidade encoraja você a utilizar as estruturas de dados nativas primeiro.

Se vocês estiver vindo de um background(?) de programação orientada a objetos, você poderá pensar que essa abordagem é estranha e retrógrado. Entretanto, você descobrirá que seus dados não precisam estar hermeticamente empacotados com um classe para que eles sejam uteis e inteligiveis. Segue um epigrama muito amado pelos Clojuristas para você pegar a visão da filosofia do Clojure:

> É melhor ter 100 funções que operam em uma única estrutura de dados do que 10 funções que operam em 10 estruturas de dados 
> - Alan Perlis

Você irá aprender mais sobre este aspecto da filosofia do Clojure nos proximos capitulos. Por enquanto, fique atento nas várias maneiras de obter reutilização de codigo ao se ater as estruturas de dados básicas.

Com isso, finalizamos nossa primeira camada de estrutura de dados. Agora é hora de nos aprofundarmos em funções e aprender como usar essas estruturas de dados!


# Funções

Uma das razões pela qual as pessoas piram nos Lisps é que essas linguagens te fazem construir programas com comportamentos complexos, mas ainda assim o seu pilar principal-a função- é tão simples. Essa seção faz a sua iniciação para a beleza e elegancia das funcoes Lisp explicando o seguinte:

- Chamada de funcoes
- Como funcoes diferem de macros e special forms
- Definicao de funcoes
- Funcoes anonimas
- Retornando funcoes


## Chamada de funções

Até o momento você ja viu varios exemplos de chamada de funcoes:
 
``` clojure
(+ 1 2 3 4)
(* 1 2 3 4)
(first [1 2 3 4])
```

Lembre-se que todas as operacoes do Clojure tem a mesma sintaxe: abre parentesis, operador, operandos, fecha parenteses. Chamadas de funcoes é apenas mais um termo para uma operacao, onde o operador é a funcao ou uma expressao de funcao (uma expressao que retorna uma funcao).

Isto te permite escrever alguns codigos bem interessantes. Segue uma expresao de funcao que retorna a funcao + (soma):

``` clojure
(or + -)
#object[clojure.core$_PLUS_ 0x1b9c1b51 "clojure.core$_PLUS_@1b9c1b51"]
```

Esse valor de retorno é a string que representa a funcao de soma. Porque o valor de retorno de OR é o primeiro valor verdadeiro e aqui a funcoao de de soma é verdadeiro, a funcao de soma é retornada. Voce também pode usar essa expressao como operador de outra expressao:

``` clojure
((or + -) 1 2 3)
; => 6
```

Porque (or + -) retorna +, essa expressao é avaliada como a soma de 1, 2 e 3, retornando 6.

Seguem mais dois exemplos de chamada de funcoes válidas que também retornam 6:

``` clojure
((and (= 1 1) +) 1 2 3)
; => 6

((first [+ 0]) 1 2 3)
; => 6
```

No primeiro exemplo, o valor de retorno de _and_ é o primeiro valor falso ou o primeiro valor verdadeiro. Nesse caso, o + é retornado porque é o ultimo valor verdadeiro, e então é aplicado aos argumentos 1 2 3, retornando 6. No segundo exemplo, o valor de retorno de _first_ é o primeiro elemento de uma sequencia, que é _+_ nesse caso.

Porém, estes não são chamadas de funcao validas, porque numero e strings nao sao funcoes:

``` clojure
(1 2 3 4)
("test" 1 2 3)
```

Se você executar esses exemplos no seu REPL, você receberá uma mensagem mais ou menos assim:

``` clojure
ClassCastException java.lang.String cannot be cast to clojure.lang.IFn
user/eval728 (NO_SOURCE_FILE:1)
```
 
É possivel que você veja esse erro muitas vezes enquanto você continuar usando Clojure: _<x> cannot be cast to clojure.lang.IFn_ simplesmente signifca que voce está tentando usar algo como funcao quando este algo nao é uma funcao.


A flexibilidade das funcoes nao termina com expressoa de funcoes! Sintaticamente, funcoes pode receber quaisquer expressoes como argumento, incluindo outras funcoes. Funcoes que podem tanto receber uma funcao como argumento ou retornar uma funcao sao chamadas de funca de ordem maior. Linguagens de programacao com funcoes de ordem maior sao conhecidas por dar suporte a funcoes de primeira classe, pois voce trata as funcoes como valores da mesmo maneira como voce trata outros tipos de dados como numeros e vetores.

Pegue a funcao map _(nao confudir com map a estrutura de dados)_, por exemplo. map cria uma nova lista ao aplicar a funcao para cada membro de uma colecao. Aqui, a funcao inc  incrementa um numero de 1 em 1:


``` clojure
(inc 1.1)
; => 2.1

(map inc [0 1 2 3])
; => (1 2 3 4)
```

(Perceba que map nao retorna um vetor, apesar de termos passado um vetor como argumento. Voce ira entender porque no Capitulo 4. Por enquanto, confia e trabalha!(?)).

Ao suportar funcoes de primeira classe, o Clojure te permite construir abstracoes mais poderosas em comparacao com  linguagens que nao as tem. Para quem nao for familiarizado com esse modo de programar, pense em funcoes como forma de permitir generalizar operacoes ao inves de estrutura de dados. Por exemplo, a funcao _+_ abstrai adiçao para quaisquer numeros especificos(?).

Por outro lado, o Clojure (e todos os Lisps) te permite criar funcoes que generalizam processos. map te permite generalizar o processo de transformar uma colecao ao aplicar a funcao - qualquer funcao - sobre qualquer colecao.

O ultimo detalhe que voce precisa saber sobre chamda de funcoes e que o Clojure avalia todos os argumentos das funcoes recursivamente antes de passa-los para a funcao. Vejamos como o Clojure avaliaria a chamada de funcao cujos argumentos tambem sao chamadas de funcoes:

``` clojure
(+ (inc 199) (/ 100 (- 7 2)))
(+ 200 (/ 100 (- 7 2))) ; avaliou "(inc 199)"
(+ 200 (/ 100 5)) ; avaliou (- 7 2)
(+ 200 20) ; avaliou (/ 100 5)
220 ; avaliou final
```

A chamada de funcao inicia o processo de avaliacao e todas as subformas sao avaliadas antes de aplicar a funca _+_.


## Chamada de funcoes, chamada de Macro e Special Forms

Na seção anterior voce aprendeu que chamada de funcoes sao expressoes que tem a expressao de uma funcao como operador. 
As outras duas formas de expressao sao chamada de macros e special forms. Voce ja viu algumas special forms: definicoes e expressoes _if_.

Voce ira aprender tudinho sobre chamadas de macro e special forms no Capitulo 7. Para o momento, a principal caracteristica que faz uma special form ser, ora, especial, é que, diferente de outras chamada de funcoes, elas nem sempre avaliam todos os seus operandos.

Pegue o _if_, or exemplo. Este é a sua estrutura geral:

``` clojure
(if boolean-form
  then-form
  optional-else-form)

```

Agora imagine que você tem um _if_ assim:

``` clojure
(if de-bom-humor
  (tweet sambinha-raiz)
  (tweet musicas-de-sofrencia))
```

Obviamente, em um ´if´ como esse, nos queremos que o Clojure avalie apenas uma das duas condições. Se o Clojure avalia ambas chamadas de função de tweet, seus seguimores do Twitter vão ficar um pouco confusos. 

Outra funcionalidade que diferencia as special forms é que você não pode usá-las como argumentos de funções. Em geral, as special forms implementam funcionalidades centrais do Clojure que simplesmente não podem ser implementadas com funções. O Clojure tem poucas special forms e é deveras incrivel que uma linguagem tão rica seja implementada com tão poucos blocos fundamentais.

As macros são parecidas com as special forms, no sentido em que elas avaliam os seus operandos diferentemente das chamadas de função e elas também não podem ser passadas como argumentos de funções. Mas esse desvio já se alongou por demais; é hora de aprender como definir funções!

## Definindo funções

Definições de funções são compostas de 5 partes principais:

- defn
- nome da função
- uma docstring descrevendo a função (opcional)
- parametros listados em colchetes
- corpo da função

Aqui temos um exemplo de uma definição de função e uma amostra da chamada da função:

```clojure 

➊ (defn super-empolgada
➋   "Retorna um incentivo que talvez seja um pouco empolgada demais"
➌   [nome]
➍   (str "OH. MEU. DEUS! " nome " VOCÊ É ABSULTAMENTE A MELHOR "
  "HOMEM BARRA MULHER, DE TODOS OS TEMPOS, EU TE AMO E A GENTE DEVERIA FUGIR PRA OUTRO LUGAR"))

(super-empolgada "Zelda")
; => "OH. MEU. DEUS! " Zelda " VOCÊ É ABSULTAMENTE A MELHOR  HOMEM BARRA MULHER, DE TODOS OS TEMPOS, EU TE AMO E A GENTE DEVERIA FUGIR PRA OUTRO LUGAR"
```

Na linha ➊ `super-empolgada` é o nome da função, que é seguido pela docstring descritiva na linha ➋. O parametro, nome, é declarado na linha ➌ e o corpo da função, na linha 4, pega o parametro é faz o que promete - retorna uma saudação que talvez seja ligeiramente super empolgada.

Vamos nos aprofundar na docstrings, parametros e corpo da função.

### A docstring

A docstring é uma maneira útil de descrever e documentar seu codigo. Você consegue ver a docstring de uma função no REPL com (doc fn-nome) - por exemplo, (doc map). A docstring também é importante caso você use alguma ferramenta para gerar documentação do seu código.


### Parametros e Aridades

As funções do Clojure podem ser definidas com zero ou mais parametros. Os valores que você passa para funções são chamados argumentos, e os argumentos podem ser de qualquer tipo. O número de parametros é a aridade da função. Seguem algumas definições de funções com diferentes aridades:

``` clojure
(defn sem-parametros
  []
  "Eu não tenho paramentros!")
(defn um-parametro
  [x]
  (str "Eu recebo um parametro: " x))
(defn dois-parametros
  [x y]
  (str "Dois parametros! Isso não é nada! Bah! Eu vou destruí-los" 
  "pra te injuriar! (?) " x y))

```

Nestes exemplos, `sem-parametros` é uma função com aridade 0, `um-parametro` tem aridade 1 e `dois-parametros` tem  aridade 2. 

Funções também suportam sobrecarga de aridade (arity overloading). Isso significa que você pode definir uma função de modo que o corpo da função a ser executado vai depender da aridade. Segue uma forma geral da definição de uma função de multiplas aridades. Perceba que cada definição de aridade está entre parenteses e tem uma lista de argumentos:

``` clojure

(defn multi-aridade
  ;; Argumento com 3 aridades e corpo da função
  ([arg-um arg-dois arg-tres]
     (fazer-coisas arg-um arg-dois arg-tres))
   ;; Argumento com 2 aridades e corpo da função
  ([arg-um arg-dois]
      (fazer-coisas arg-um arg-dois -tres))
   ;; Argumento com 1 aridade e corpo da função
  ([arg-um]
      (fazer-coisas arg-um )))
```

Sobrecarga de aridade é uma maneira de prover valores padrões para argumentos. No exemplo a seguir `"karatê"` é o argumento padrão para o parametro `tipo-do-golpe`:


``` clojure
(defn golpe-x
  "Descrive o tipo de golpe que você vai dar em alguém."
  ([nome tipo-de-golpe]
     (str "Eu dou o golpe:" tipo-de-type " em " nome "! Receba!"))
  ([nome]
     (golpe-x nome "karate")))

```

Se você chamar `golpe-x` com dois argumentos, a função funciona como deveria se não fosse uma funcao de de multiplas aridades:

```clojure
(golpe-x "Kanye West" "tapa")
; => "Eu dou o golpe: tapa em Kanye West! Receba!"
```

Se você chamar `golpe-x` somente com um argumento, `golpe-x` vai se autochamar com o segundo argumento `karate`que foi definido:

```clojure
(golpe-x "Kanye West")
; => "Eu dou o golpe: karate em Kanye West! Receba!"
```
![a black and white illustration of Kanye West at a table with some vegetables and pushing a pump dispenser. ](imagens/kanye.png)

Pode parecer nao muito comum definir uma funcao dessa forma, em termos dela mesma. Se sim, ótimo! Isso significa que você está aprendendo uma nova maneira de fazer coisas!  

Você també pode definir que cada aridade faça algo completamente diferente entre si:

```clojure

(defn aridade-estranha
  ([]
  "O destino te vestiu essa manhã, meu amigo, e agora o Medo está tentado tirar as suas calças. Se você desistir, se você ceder, você sempre acabará pelado com o Medo rindo das suas vergonhas - O Tick")
  ([numero]
     (inc numero)))
```

O corpo da função de aridade zero retorna uma frase sábia e o corpo de aridade um aumenta o valor em 1 unidade do número. Muito provavelmente você não vai querer escrever uma função assim, porque poderia ser confuso ter dois corpos de  função que são totalmente nao relacionados.

O Clojure também te permite funções com aridades variaveis ao incluir um _parametro rest_, tipo "coloque o _resto_ desses argumentos em uma lista com seguinte nome". O parametro _rest_ é indicado por um "e comercial" (`&`), como vemos no ➊:


``` clojure
(defn xingamento-de-velhote
  [moleque]
  (str "Saia do meu gramado, " moleque "!!!"))

(defn velhote
➊   [& moleque]
  (map xingamento-de-velhote moleque))

(velhote "Cleitn" "'Na Maria" "O Incrivel Bulk")
; => ("Saia do meu gramado, Cleitin!!!"
      "Saia do meu gramado, 'Na Maria!!!"
      "Saia do meu gramado, O Incrivel Bulk!!!")
```

![A imagem retrata um velhinho rabugento com uma bengala, expressando frustração com a frase "Xinguem tudo até a morte!", e junto dele está um cachorrinho dachshund vestindo um suéter e uma cartola.](velhinho.png)

Como você pode ver, quando você passa argumentos para funções com aridade variável, os argumentos são tratados como uma lista. Você consegue misturar parametros _rest_ com parametros normais, mas os parametros rest tem que vir por ultimo:

``` clojure
(defn coisas-favoritas
[nome & coisas]
(str "Oier, " nome ", aqui estão as minhas coisas favoritas: "
(clojure.string/join ", " coisas)))

(coisas-favoritas "Dorinha" "chiclete" "sapatos" "kara-tê")
; => "Oier, Dorinha, aqui estão as minhas coisas favoritas: chiclete, sapatos, kara-tê"
```

Finalmente, o Clojure tem uma maneira mais sofisticada de definir parametros, chamada _destructuring_ (desestruturação), a qual merece sua própria subseção.

### Destructuring

A idéia basica por trás de _destructuring_ é que ela te permite associar , de forma concisa, valores a nomes dentro de uma coleção. Vejamos um exemplo básico:


``` clojure 
;Retorna o primeiro elemento de uma coleção
(defn minha-primeira
[[primeira-coisa]] ; Perceba qie primeira-coisa está dentro de um vetor
primeira-coisa)

(minha-primeira ["forno" "bicicleta" "machado de guerra"])
; => "forno"
```

Aqui, a função `minha-primeira` associar o símbolo `primeira-coisa` com o primeiro elemento do vetor que foi passado como argumento. Você diz para `minha-primeira` fazer isso ao colocar o simbolo dentro de um vetor.

Esse vetor é como um simbolo grandão levantado para o Clojure que diz:“Ei! Esta função vai receber uma lista ou um vetor como argumento. Facilite minha vida desmembrando a estrutura do argumento para mim e associando nomes significativos às diferentes partes do argumento!”. Quando você desestrutura um vetor ou uma lista, você pode nomear quantos elementos quiser e também usar parametros _rest_:

``` clojure
(defn seletor
[[primeira-escolha, segunda-escolha e escolhas-desimportantes]]
(println (str "Sua primeira escolha é: " primeira-escolha))
(println (str "Sua segunda escolha é: " segunda-escolha))
(println (str "Estamos ignorando o resto das suas escolhas. "
"Aqui estão elas, caso você precise chorar por elas: "
(clojure.string/join ", " escolhas-desimportantes))))

(seletor ["Geleia", "Jack Bonitão", "Chiqueirinho", "Aquaman"])
; => Sua primeira escolha é: Geleia
; => Sua segunda escolha é: Jack Bonitão
; => Estamos ignorando o resto das suas escolhas. Aqui estão elas, caso você precise chorar por elas: Chiqueirinho, Aquaman
```

Aqui, o parametro _rest_ `escolhas-desimportantes` lida com qualquer numero adicional de escolhas do usuário, após a primeira e segunda.

Você também pode desestruturar mapas. Da mesma maneira que você diz pro Clojure desestruturar um vetor ou lista, fornecendo um vetor como parametro, você desestrutura mapas ao fornecer um mapa como parametro:

``` clojure
(defn anunciar-localizacao-do-tesouro
➊   [{lat :lat lng :lng}]
  (println (str "Lat do tesouro: " lat))
  (println (str "Lng do tesouro: " lng)))

(anunciar-localizacao-do-tesouro {:lat 28.22 :lng 81.33})
;"Lat do tesouro: 28.22"
;"Lng do tesouro: 81.33"
```

Vamos analisar a linha em ➊ com mais detalhes. É como dizer ao Clojure, "Clojure, mano! Quebra essa pra mim e associe o nome `lat` com o valor correspondente a chave `:lat`. Faz o mesmo pra `lgn` e `:lng`. Flw, vlw!"

Com uma certa frequencia a gente so quer separar as keywords de um mapa, então existe uma sintaxe mais curta para isso. Este tem o mesmo resultado que o exemplo anterior:


``` clojure
(defn anunciar-localizacao-do-tesouro
➊   [{:keys lat lng}]
  (println (str "Lat do tesouro: " lat))
  (println (str "Lng do tesouro: " lng)))
``` 

Você pode reter acesso ao mapa original do argumento usando a keyword `:as`. No exemplo a seguir, o mapa orignal é acessado com `localizacao-do-tesouro`:

```clojure
(defn receber-localizacao-do-tesouro
  [{:keys [lat lng] :as localizacao-do-tesouro}]
  (println (str "Lat do tesouro: " lat))
  (println (str "Lng do tesouro: " lng))

  ;;Poderia-se supor que isso definiria novas coordenadas para seu navio.
  (pilotar-navio! localizacao-do-tesouro))
```

Em geral, você pode pensar em desestruturação como instruir o Clojure em como associkar nomes com valores em uma lista, mapa, conjunto ou vetor. Agora, vamos para a parte da função que de fato faz algo: o corpo da função! 

### Corpo da Função

O corpo da função pode conter qualquer tipo de forma. O Clojure automaticamente retorna a ultima forma avaliada. Este corpo da função contém apenas três formas, e quando você chama a função, ele cospe fora a última forma `"joe"`:

``` clojure
(defn funcao-ilustrativa
[]

(+ 1 304)
30
"joe")


(funcao-ilustrativa)
; => "joe"
```

Segue mais outro corpo de função que usa a expressção `if`:

``` clojure
(defn comentar-numero
  [x]
  (if (> x 6)
    "Minha nossa! Que númerão!"
    "Esse número é ok, acho..."))

(comentar-numero 5)
; => "Esse número é ok, acho..."

(comentar-numero 7)
; => "Minha nossa! Que númerão!"

```

### Todas as funções são criadas iguais

Uma nota final: o Clojure não tem funções privilegiadas. `+` é só uma função, `-`  é só uma função é `inc` e `map`  são só funções. Elas não são melhores do que as funções que você define. Portanto, não deixe que elas te respondam com insolência!

Mais importante ainda, este fato ajuda a demonstrar a simplicidade inerente do Clojure. De um certo modo o Clojure é bem burrinho. Quando você faz uma chamada de função, o Clojure apenas diz "`map`? Claro, que seja! Eu vou só aplicar isso e seguir em frente." Ele não se importa que função seja ou de onde veio; ele trata todas as funções da mesma maneira. No seu cerne, o Clojure não dá a mininma sobre adição, multipliocação ou mapeamento. Ele só se importa em aplicar funções.

À medida que você continua a programar com Clojure, você vai ver que essa simplicidade é ideal. Você não precisa se preocupar com regras ou sintaxes especiais para trabalhar com diferentes funções. Todas funcionam da mesma maneira!

## Funções anônimas

Em Clojure, funções não precisam ter nomes. De fato, você irá usar funções _anônimas_ o tempo todo. Que misterioso! Você pode criar funções anônimas de dois jeitos. A primeira é usar a forma `fn`:

``` clojure
(fn [lista-de-paramentros]
corpo da função)
```

Parece bastante com `defn`né? Vamos tentar dois exemplos:

```clojure 
(map (fn [nome] (str "Olá, " nome))
["Darth Vader" "Mr. Magoo"])

; => ("Olá, Darth Vader" "Olá, Mr. Magoo")

((fn [x] (* x 3)) 8)
; => 24
```

Você pode tratar `fn` praticamente identicamente da maneira que você trata `defn`. A lista de parametros e corpos da função funcionam exatament da mesma maneira. Você poide usar desestruturação de argumento, parametros rest e por ai vai. Você pode até mesmo associar sua função anonima com um nome, o que não deveria causar surpresa (mas se causou surpresa, bem... Surpresa!):

```clojure
(def meu-multiplicador-especial (fn [x] (* x 3)))
(meu-multiplicador-especial 12)
; => 36
```

O Clojure também oferece outro jeito mais compacto de criar funções anônimas. Veja como é uma função anônima:

```clojure

#(* % 3)
```

Nossa, isso parece estranho. Vá em frente e aplique essa função estranha:

```clojure
(#(* % 3) 8)
; => 24
```

Segue um exemplo de como passar uma função anônima como argumento para a função map:

```clojure
(map #(str "Olá, " %)
["Darth Vader" "Mr. Magoo"])

; => ("Olá, Darth Vader" "Olá, Mr. Magoo"))
```

Esse estilo estranhão de escrever funções anônimas é possível através de uma funcionalidade chamada _reader macros_. Você aprenderá sobre elas no Capítulo 7. Por agora é de boa só aprender como usar essas funções anônimas.

Você pode perceber que essa sintaxe é definitivamente mais compacta, mas também um pouco estranha. Vamos ver por parte. Esse tipo de função anônima se parece muito com uma chamada de função, exceto pelo fato de ser precedida por uma cerquilha, `#`:

```clojure
;; Chamada de função
(* 8 3)

;; Função anônima
#(* % 3)
```

Essa semelhança permite que você veja mais rapidamente o que acontecerá quando essa função anonima é aplicada. "Oh," você pode dizer para si, "isto irá multiplicar o argumento por três." 

Como você já deve ter adivinhado, o simbolo de porcentagem `%`, indica o argumento passado para a função. Se suas funções anonimas recebem múltiplos argumentos, você pode diferenciá-los dessa forma: `%1`, `%2`, `%3`, e assim por diante. `%` é equivalente a `%1`:

``` clojure 
(#(str %1 " e " %2) "pão de milho" "feijão manteiga")
; => "pão de milho e feijão manteiga"

```


Você também pode passar parametros _rest_ com `%`:

```clojure 
(# (identity %1)1 "bleh" :hey)
; => (1 "bleh" :hey)
```

Neste caso, você aplicou a função _identity_ ao argumento _rest_. 
_Identity_ retorna o argumento que é dado sem alterá-lo. Argumentos _rest_ são armazenados como listas, então a aplicação da função retorna uma lista de todos os argumentos.

Se você precisa escrever uma função anônima simples, usar esse estilo é melhor por causa do seu impacto visual. Por outro lado, isso pode facilmente se tornar ilegível se você estiver escrevendo uma função mais longa e mais complexa. Se esse for o caso, use `fn`.

## Retornando Funções

Por agora você já viu que funções podem retornar outra funções. As funções retornadas são _closures_, o que significa que elas podem acessar todas as variáveis que estavam no escopo quando a função foi criada. Aqui está um exemplo padrão:

```clojure
(defn fazedor-de-soma
  "Cria um incrementador personalizado"
  [somar-por]
  #(+ % somar-por))

(def soma3 (fazedor-de-soma 3))

(soma3 7)
; => 10
```
Aqui, `somar-por` está no escopo, então a função retornada tem acesso a isso, mesmo quando a função retornada está fora do `fazedor-de-soma`.

## Juntando tudo

Okay! É hora de você usar o seu conhecimento recém adquirido para um nobre propósito: abater hobbits! Para bater em um hobbit, você primeiramente irá modelar as partes do corpo dele. Cada parte do corpo incluirá o seu tamanho relativo para indicar a possibilidade de ela ser atingida. Para evitar repetição, o modelo do hobbit irá incluir apenas entradas para _pé esquerdo_, _orelha esquerda_, e assim por diante. Portanto, você precisará de uma função para simetrizar integralmente o modelo, e criar _pé direito_, _orelha direita_ e assim por diante. Por ultimo, você criará uma função que itera pelas partes do corpo e aleatoriamente escolhe onde atingir. Ao longo do caminho, você aprenderá sobre algumas novas ferramentas do Clojure: expressões `let`, loops e expressões regulares. Que divertido!

## O proximo top model do Condado dos Hobbits

Para o nosso modelo de hobbit, vamos evitar características como jovialidade e travessura, focando apenas no pequenino corpo do hobbit. Aqui está o modelo do hobbit:

``` clojure
(def partes-do-corpo-de-hobbit-assimétrico  
[{:nome "cabeça" :tamanho 3}
{:nome "olho-esquerdo" :tamanho 1}
{:nome "orelha-esquerda" :tamanho 1}
{:nome "boca" :tamanho 1}
{:nome "nariz" :tamanho 1}
{:nome "pescoço" :tamanho 2}
{:nome "ombro-esquerdo" :tamanho 3}
{:nome "braço-esquerdo" :tamanho 3}
{:nome "peito" :tamanho 10}
{:nome "costas" :tamanho 10}
{:nome "antebraço-esquerdo" :tamanho 3}
{:nome "abdômen" :tamanho 6}
{:nome "rim-esquerdo" :tamanho 1}
{:nome "mão-esquerda" :tamanho 2}
{:nome "joelho-esquerdo" :tamanho 2}
{:nome "coxa-esquerda" :tamanho 4}
{:nome "perna-esquerda" :tamanho 3}
{:nome "tendão-de-aquiles-esquerdo" :tamanho 1}
{:nome "pé-esquerdo" :tamanho 2}])
```

Este é um vetor de mapas. Cada mapa tem o nome da parte do corpo e tamanho relativo à parte do corpo. (Eu sei que só personagens de anime têm olhos com um terço do tamanho da cabeça, mas relevem, tá?)

O que chama a atenção é a ausência do lado direito do hobbit. Vamos arrumar isso. O bloco de código 3-1 é o mais complexo que você já viu até agora, e ele introduz algumas ideias novas. Mas não se preocupe, porque iremos examiná-lo nos mínimos detalhes!

``` clojure
(defn parte-correspondente)
[parte]
{:nome (clojure.string/replace (:nome parte) #"^esquerda-" "direita-")
 :tamanho (:tamanho parte))}

(defn simetrizar-partes-do-corpo
"Espera uma sequência de mapas que possuem um :nome e um :tamanho"
[partes-do-corpo-assimetricas]
(loop [partes-assimetricas-restantes partes-do-corpo-assimetricas
partes-do-corpo-finais []]
(if (empty? partes-assimetricas-restantes)
  partes-do-corpo-finais
  (let [[parte & restantes] partes-assimetricas-restantes]
   (recur restantes
          (into partes-do-corpo-finais
                (set [parte (parte-correspondente parte)])))))))
```

_3-1. As funções parte-correspondente e simetrizar-partes-do-corpo_

Quando chamamos a função `simetrizar-partes-do-corpo` em `partes-do-corpo-de-hobbit-assimétrico`, obtemos um hobbit totalmente simétrico:
```clojure
(simetrizar-partes-do-corpo partes-do-corpo-de-hobbit-assimétrico)
; => [{:nome "cabeça", :tamanho 3}
{:nome "olho-esquerdo", :tamanho 1}
{:nome "olho-direito", :tamanho 1}
{:nome "orelha-esquerda", :tamanho 1}
{:nome "orelha-direita", :tamanho 1}
{:nome "boca", :tamanho 1}
{:nome "nariz", :tamanho 1}
{:nome "pescoco", :tamanho 2}
{:nome "ombro-esquerdo", :tamanho 3}
{:nome "ombro-direito", :tamanho 3}
{:nome "braco-esquerdo", :tamanho 3}
{:nome "braco-direito", :tamanho 3}
{:nome "peito", :tamanho 10}
{:nome "costas", :tamanho 10}
{:nome "antebraco-esquerdo", :tamanho 3}
{:nome "antebraco-direito", :tamanho 3}
{:nome "abdomen", :tamanho 6}
{:nome "rim-esquerdo", :tamanho 1}
{:nome "rim-direito", :tamanho 1}
{:nome "mao-esquerda", :tamanho 2}
{:nome "mao-direita", :tamanho 2}
{:nome "joelho-esquerdo", :tamanho 2}
{:nome "joelho-direito", :tamanho 2}
{:nome "coxa-esquerda", :tamanho 4}
{:nome "coxa-direita", :tamanho 4}
{:nome "perna-esquerda", :tamanho 3}
{:nome "perna-direita", :tamanho 3}
{:nome "tendao-de-aquiles-esquerdo", :tamanho 1}
{:nome "tendao-de-aquiles-direito", :tamanho 1}
{:nome "pe-esquerdo", :tamanho 2}
{:nome "pe-direito", :tamanho 2}]

```

Vamos analisar esse código!

## let

No meio da loucura da Listagem 3-1 você pode ver a forma de uma estrutura `(let ...)`. Vamos construir um entendimento do `let`um exemplo por vez, e depois examinar o exemplo completo do programa quando tivermos familiarizados com todas as peças.

`let` associa nomes a valores. Você pode pensar no `let`como abreviação para "deixa a vida me levar, vida leva eu" (_let it be_), que é uma linda canção do Zeca... digo, dos Beatles, sobre programação. Aqui vai um exemplo:

``` clojure 
(let [x 3]
  x)
; => 3

(def lista-de-dalmatas
  ["Florzinha" "Perdigueiro" "Auau 1" "Auau 2"])
(let [dalmatas (take 2 lista-de-dalmatas)]
  dalmatas)
; => ("Florzinha" "Perdigueiro")
```
No primeiro exemplo, você associa o nome `x` ao valor `3`. No segundo, você associa o nome `dalmatas` ao resultado da expressão ` (take 2 lista-de-dalmatas)`, que era a lista `("Florzinha" "Perdigueiro")`. `let` também introduz um novo _escopo_:

``` clojure 
(def x 0)
(let [x 1] x)
; => 1
```

Aqui, primeiro você associa o nome `x` ao valor `0` usando `def`. Dai, `let` cria um novo escopo no qual o nome `x` é associado ao valor `1`. Eu penso no escopo como o contexto ao qual algo se refere. Por exemplo, na frase _por favor limpe essa sujeira_, sujeira significando algo diferente dependendo se você trabalha numa maternidade ou como zelador de uma conferência de fabricantes de cigarros. Nesse trecho de código você está dizendo, "Eu quero que `x` seja `0` no contexto global, mas dentro do contexto dessa expressão `let`, ele deve ser `1`."

Você pode referenciar associações existentes na sua associação `let`:

```clojure

(def x 0)
(let [x (inc x)] x)
; => 1
```

Nesse exemplo, o `x` em `(inc x)` refere-se a associação criada por `(def x 0)`. O valor resultante é `1`, o qual é então associados ao nome `x` dentro do novo escopo criado pelo `let`. Dentro das delimitações da forma `let`, `x` se refere a `1`, não a `0`.

Você também pode usar os parametros _rest_ no `let`, assim como você pode em funções:


```clojure 
(let [[florzinha & dalmatas] lista-de-dalmatas]
  [florzinha dalmatas])
; => ["Florzinha" ("Perdigueira" "Auau 1" "Auau 2")]

```

