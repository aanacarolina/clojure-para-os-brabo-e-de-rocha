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


