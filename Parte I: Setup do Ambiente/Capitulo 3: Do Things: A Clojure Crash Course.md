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


