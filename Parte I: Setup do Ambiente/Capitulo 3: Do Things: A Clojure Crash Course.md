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
(get ["a" {:name "Pugsley Winterbottom"} "c"] 1)
; => {:name "Pugsley Winterbottom"}
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
 
É possivel que você veja esse erro muitas vezes enquanto você continuar usando Clojure: _<x> cannot be cast to clojure.lang.IFn_ simplesmente signifca que voce está tentando usar algo como funcoao quando este algo nao é uma funcao.
