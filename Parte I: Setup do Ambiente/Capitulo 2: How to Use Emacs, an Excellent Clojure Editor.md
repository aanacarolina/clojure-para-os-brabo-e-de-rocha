### *Capítulo 2: Como usar o Emacs, um ótimo editor de código para Clojure*
Na sua jornada para se tornar um mestre do Clojure, o seu editor será o seu aliado mais próximo. Eu recomendo fortemente trabalhar com o Emacs, mas você pode, claro, usar qualquer editor que preferir. Se você não seguir as instruções detalhadas sobre o Emacs neste capitulo, ou se você escolher usar um editor diferente, vale a pena ao menos investir algum tempo configurando o seu editor para trabalhar com um REPL. Duas alternativas que eu recomendo e que são bem avaliadas na comunidade são [Cursive](https://cursive-ide.com/) e [NightCode](https://github.com/oakes/Nightcode).

O motivo da minha recomendação do Emacs é que ele oferece uma boa integração com o REPL do Clojure, o qual te permite rodar o seu código instantaneamente enquanto você o escreve. Essa possibilidade de feedback rápido vai ser útil enquanto você estiver aprendendo clojure e depois quando estiver escrevendo programas Clojure de verdade. O Emacs também é ótimo para trabalhar com qualquer dialeto Lisp, na verdade, o Emacs é escrito num dialeto Lisp chamado Emacs Lisp. (elisp). 

Ao final deste capítulo as suas configurações do Emacs vão estar mais ou menos assim:

![img2-1.png](../imagens/img2-1.png)

*Imagem 2-1: Uma típica configuração do Emacs com o código Clojure de um lado e o REPL do outro*

Para chegar lá, você vai começar instalando o Emacs e adicionar uma configuração amigável para pessoas iniciantes. Então, você irá aprender o básico: Como abrir, editar, salvar arquivos e como interagir com o Emacs usando atalhos do teclado essenciais. Por último você irá aprender como de fato editar um código Clojure e interagir com o REPL.

## Instalando o Emacs
Você deverá usar a última versão major do Emacs, Emacs 24, para a plataforma que você estiver utilizando: 
- **OS X** Instale o Emacs padrão como aplicativo do Mac da página no [Emacs para Mac OS X](https://emacsformacosx.com/). Outras opções como Aquamacs deveriam deixar o Emacs com uma carinha de Mac, mas ao longo prazo eles são problemáticos, porque as configurações são tão diferentes do Emacs padrão que fica difficile seguir o manual ou tutoriais do Emacs.
- **Ubuntu** Siga as instruções de instalação do [Emacs no Ubuntu](https://www.gnu.org/software/emacs/download.html#ubuntu). (confirmar se o link está correto????)
- **Windows** Você encontra o arquivo binário em [Emacs para Windows](https://ftp.gnu.org/gnu/emacs/windows/). Após baixar o arquivo, e descompactar a última versão você pode rodar o executable do Emacs que está na pasta `bin\runemacs.exe`.

Após instalar o Emacs, abra o aplicativo e veja se tudo está funcionando. Você deve ver uma tela inicial como a imagem abaixo:

![img2-2.png](../imagens/img2-2.png)
*Imagem 2-2: A tela inicial do Emacs*

Seja bem vindo ao culto do Emacs! Você deixou o Richard Stallman orgulhoso!