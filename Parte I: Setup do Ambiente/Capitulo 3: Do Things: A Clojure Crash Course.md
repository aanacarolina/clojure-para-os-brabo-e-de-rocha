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
verdadeiro ou falso. Você irá aprender sobre veracidade ou falsidade na proxima seção. Segue mais um par de exemplos de *if*:

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

Você também pode omitir o bloco do `else`. Se você fizer isso e a expressão Booleana for `false, o Clojure retorna `nil`, dessa forma:

```clojure
(if false
  "Pelo cotovelo de Odin!")
; => nil
```



