# git
Utilizando Git para versionamento e trabalho em equipe
Version Control System (VCS) Git e GitHub não são a mesma coisa.
O Git foi criado durante a escrita do novo kernel do linux, nos anos 2000 Linus Tovalt, para controlar seus contribuidores.

Para comerçar a trabalhar com o Git é necessário primeiramente fazer sua instalação, conforme seu SO:

https://git-scm.com/downloads

###Instalando e configurando o Git

Existem maneiras de interagir além do terminal de nosso computador, mas aqui abordaremos praticamente somente comando via terminal.

Configurar credencias, para identificação das contribuições em projetos:
Configurando o nome que será mostrado em nosso commits
```terminal
git config --global user.name "Lucas Alberto"
```
Configurando email
```terminal
git config --global user.email "lucas@mail.com"
```
Conferindo nossas credenciais
```terminal
git config --global --list
```
``` terminal
C:\Users\Lucas\Desktop>git config --global --list
user.name=Lucas Alberto
user.email=lucas@mail.com
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
```

Conferindo todas as nossas informações
```terminal
git config --list
```
Para iniciar um novo projeto com Git:
Dentro do diretório a ser inicializado:
``` terminal
C:\Dev\iniciando-com-git>git init
Initialized empty Git repository in C:/Dev/iniciando-com-git/.git/
```

Clonando um projeto remoto para nosso computador
git clone projeto destino
A autenticação poderá ser solicitada duarante o processo.

``` terminal
C:\Users\Lucas\Desktop>git clone https://github.com/lschlestein/ExerciciosJava ExerciciosJava
Cloning into 'ExerciciosJava'...
info: please complete authentication in your browser...
remote: Enumerating objects: 27, done.
remote: Counting objects: 100% (27/27), done.
remote: Compressing objects: 100% (24/24), done.
remote: Total 27 (delta 0), reused 27 (delta 0), pack-reused 0
Receiving objects: 100% (27/27), 6.64 KiB | 3.32 MiB/s, done.
```

O simples fato de termos clonado um repositório remoto, não nos garante o sincronismo do nosso projeto local com o remoto.
É necessário que façamos o controle desse sincronismo
Fluxo de trabalho: Working Dir, Stage (Palco) e Head
![image](https://github.com/lschlestein/git/assets/103784532/740f6a2e-74b1-4cca-a4da-1f2776288201)

Os arquivos editados ou criados em nosso Working Dir, serão indexados ou adicionados ao Stage(Palco).
Apartir do momento que adicionamos um arquivos ao Stage, caso o arquivo de nosso Working dir seja modificado, essa mudança não afetará nosso arquivos já indexados.
Logo em seguida podemos fazer o Commit. A partir desse momento, geramos um histórico de mudança e adicionamos esse arquivo ao nosso Git Repository. Após o Commit (confirmação), o arquivo deixa o Stage
![image](https://github.com/lschlestein/git/assets/103784532/27693f24-11ee-476b-8df7-445925eb48f8)

#Adicionar e Remover Arquivos, Uso do Status e do Diff

``` git
C:\Users\Lucas\Desktop\iniciando-com-git>git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        index.html
        script.js
        style.css
```

Para adicionar arquivos ao Stage, podemos adicionar um a um:

C:\Users\Lucas\Desktop\iniciando-com-git>git add index.html

ou todos de uma só vez, que ainda não estão no Stage
C:\Users\Lucas\Desktop\iniciando-com-git>git add .
C:\Users\Lucas\Desktop\iniciando-com-git>git add *.css

Atualiza quem ainda não entrou no Stage
C:\Users\Lucas\Desktop\iniciando-com-git>git add -A

mostra quais arquivos estão dentro e fora do Stage
git status

Retirar do stage e trazer devolta para nosso Working dir
git reset index.html

Para restaurar um arquivo que está no Stage para no Working Dir:
git restore index.html

Vamos adicionar um rodapé ao index.html
Comparando as diferenças, entre nosso Working Dir e o Stage
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git diff index.html
diff --git a/index.html b/index.html
index 5d3469b..126ad9f 100644
--- a/index.html
+++ b/index.html
@@ -9,4 +9,9 @@
 <br/>
 <a href="hello-servlet">Hello Servlet</a>
 </body>
+<footer>
+    <p>
+        Desenvolvido por Lucas
+    </p>
+</footer>
 </html>
\ No newline at end of file

C:\Users\Lucas\Desktop\iniciando-com-git>git diff
diff --git a/index.html b/index.html
index 5d3469b..a561cf5 100644
--- a/index.html
+++ b/index.html
@@ -8,5 +8,11 @@
 </h1>
 <br/>
 <a href="hello-servlet">Hello Servlet</a>
+
+<footer>
+    <p>
+        Desenvolvido por Lucas
+    </p>
+</footer>
 </body>
 </html>
\ No newline at end of file
```

Criando um Commit
Um Commit, nada mais é que um Snapshot de nosso projeto, que será feito no momento que fazemos a confirmação. (Alterações, Hash, Metadados, Mensagem)
- Cria rastreamento de alterações
- Evita sobreescrita de código

Primeiro Commit
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git commit -m "Primeiro Commit Git"
[master (root-commit) c93cfe8] Primeiro Commit Git
 3 files changed, 18 insertions(+)
 create mode 100644 index.html
 create mode 100644 script.js
 create mode 100644 style.css
```



