# git
Utilizando Git para versionamento e trabalho em equipe
Version Control System (VCS) Git e GitHub não são a mesma coisa.
O Git foi criado durante a escrita do novo kernel do linux, nos anos 2000 Linus Tovalt, para controlar seus contribuidores.

Para comerçar a trabalhar com o Git é necessário primeiramente fazer sua instalação, conforme seu SO:

https://git-scm.com/downloads

### Instalando e configurando o Git

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

Após o Commit, os arquivos deixam o Stage
É possível fazer o Commit de um mais arquivos, sem adicioná-los previamente ao Stage com o seguinte comando
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git commit -a -m "Atualização do H1"
[master c591b37] Atualização do H1
 1 file changed, 1 insertion(+), 1 deletion(-)
```
Caso seja necessário alterar novamente um arquivo no último Commit feito, é possível utilizando o comando amend
```terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git commit --amend -m "H1 modificado. Alterando último Commit"
[master ebe5e11] H1 modificado. Alterando último Commit
 Date: Wed Jun 5 12:09:56 2024 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

É possível mostrar as diferenças entre o último Commit e os arquivos do Stage
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git diff --staged
diff --git a/index.html b/index.html
index 71f2f62..ca96b3c 100644
--- a/index.html
+++ b/index.html
@@ -4,7 +4,7 @@
     <title>JSP - Hello World</title>
 </head>
 <body>
-<h1><%= "Hello World! Commit" %>
+<h1><%= "Hello World! 2055" %>
 </h1>
 <br/>
 <a href="hello-servlet">Hello Servlet</a>
```
Boas práticas com mensagens de Commits iniciando com
-ADD
-FIX
-CHANGE
-UPDATE

Logs e Histórico
git log

``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git log
commit ebe5e1136e621625bf0c2a623b954e093cd17bb3 (HEAD -> master)
Author: Lucas Alberto <lschlestein@gmail.com>
Date:   Wed Jun 5 12:09:56 2024 -0300

    H1 modificado. Alterando último Commit

commit c93cfe8720e1960cf82be151233b719d2b9de43d
Author: Lucas Alberto <lschlestein@gmail.com>
Date:   Wed Jun 5 12:03:51 2024 -0300
```

Simplificando o log em uma única linha

``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git log --oneline
ebe5e11 (HEAD -> master) H1 modificado. Alterando último Commit
c93cfe8 Primeiro Commit Git
```

Limitando aos últimos 5 commits

``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git log --oneline -5
ebe5e11 (HEAD -> master) H1 modificado. Alterando último Commit
c93cfe8 Primeiro Commit Git
```
Utilizando o graph
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git log --graph
* commit ebe5e1136e621625bf0c2a623b954e093cd17bb3 (HEAD -> master)
| Author: Lucas Alberto <lschlestein@gmail.com>
| Date:   Wed Jun 5 12:09:56 2024 -0300
|
|     H1 modificado. Alterando último Commit
|
* commit c93cfe8720e1960cf82be151233b719d2b9de43d
  Author: Lucas Alberto <lschlestein@gmail.com>
  Date:   Wed Jun 5 12:03:51 2024 -0300

      Primeiro Commit Git
```

Filtrando por autor
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git log --author="Lucas"
commit ebe5e1136e621625bf0c2a623b954e093cd17bb3 (HEAD -> master)
Author: Lucas Alberto <lschlestein@gmail.com>
Date:   Wed Jun 5 12:09:56 2024 -0300

    H1 modificado. Alterando último Commit

commit c93cfe8720e1960cf82be151233b719d2b9de43d
Author: Lucas Alberto <lschlestein@gmail.com>
Date:   Wed Jun 5 12:03:51 2024 -0300
```

Shortlog
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git shortlog
Lucas Alberto (2):
      Primeiro Commit Git
      H1 modificado. Alterando último Commit
```

Reflog - Ações no repositório
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git reflog
ebe5e11 (HEAD -> master) HEAD@{0}: commit (amend): H1 modificado. Alterando último Commit
c591b37 HEAD@{1}: commit: Atualização do H1
c93cfe8 HEAD@{2}: commit (initial): Primeiro Commit Git
```

Branch
Caminho alternativo ao Branch principal
Copia completa do repositório inteiro pra outra branch.

Criando uma nova branch
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git branch dev
```
Mostrando as branchs de um repositório
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git branch
  dev
* master
```
Deletando uma branch
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git branch -D dev
Deleted branch dev (was d2a293e).
```
Mudando de branch (Muda para a branch dev, e como ela ainda não existe, já fará sua criação nesse mesmo instante)
Checkout faz a navegação entre as branchs
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git checkout -b dev
Deleted branch dev (was d2a293e).
```
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git branch
* dev
  master
```

Para renomear a branch atual
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git branch -m "develop"

C:\Users\Lucas\Desktop\iniciando-com-git>git branch
* develop
  master
```

Podemos agora olhar o log de ambas as branchs, e veremos que os dois são identicos
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git log --oneline master
d2a293e (HEAD -> develop, master) Atualizada a linguagem da página
04c8b92 Atualizado H1
ebe5e11 H1 modificado. Alterando último Commit
c93cfe8 Primeiro Commit Git

C:\Users\Lucas\Desktop\iniciando-com-git>git log --oneline develop
d2a293e (HEAD -> develop, master) Atualizada a linguagem da página
04c8b92 Atualizado H1
ebe5e11 H1 modificado. Alterando último Commit
c93cfe8 Primeiro Commit Git
```

Agora vamos fazer um Commit na branch develop
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git add index.html

C:\Users\Lucas\Desktop\iniciando-com-git>git status
On branch develop
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html

C:\Users\Lucas\Desktop\iniciando-com-git>git status
On branch develop
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html

C:\Users\Lucas\Desktop\iniciando-com-git>git commit -m "Adiciona assets"
[develop 420bdf9] Adiciona assets
 1 file changed, 2 insertions(+)
```
Agora podemos comparar novamente as duas branchs
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git log --oneline develop
420bdf9 (HEAD -> develop) Adiciona assets
d2a293e (master) Atualizada a linguagem da página
04c8b92 Atualizado H1
ebe5e11 H1 modificado. Alterando último Commit
c93cfe8 Primeiro Commit Git

C:\Users\Lucas\Desktop\iniciando-com-git>git log --oneline master
d2a293e (master) Atualizada a linguagem da página
04c8b92 Atualizado H1
ebe5e11 H1 modificado. Alterando último Commit
c93cfe8 Primeiro Commit Git
```
Fica claro que só estamos alterando a branch develop

Verificando diferenças entre as branchs
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git diff master develop
diff --git a/index.html b/index.html
index 8d51d33..6d48536 100644
--- a/index.html
+++ b/index.html
@@ -2,6 +2,8 @@
 <html lang="pt-br">
 <head>
     <title>JSP - Hello World</title>
+    <link rel="stylesheet" href="style.css"/>
+    <script src="script.js"></script>
 </head>
 <body>
 <h1><%= "Hello World! 2034" %>
```
Umas das vantagens do Git é agrupar todo desenvolvimento em um servidor central, com vários colaboradores.


Remote no GitHub
```terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git remote add origin https://github.com/lschlestein/iniciando-com-git.git

C:\Users\Lucas\Desktop\iniciando-com-git>git remote -v
origin  https://github.com/lschlestein/iniciando-com-git.git (fetch)
origin  https://github.com/lschlestein/iniciando-com-git.git (push)
````
Nota-se que origin é o nome da nossa brabch remota

Subindo push nosso projeto para nosso repositório no GitHub (Origin<-Develop)
``` terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git push -u origin develop
Enumerating objects: 24, done.
Counting objects: 100% (24/24), done.
Delta compression using up to 8 threads
Compressing objects: 100% (23/23), done.
Writing objects: 100% (24/24), 2.90 KiB | 990.00 KiB/s, done.
Total 24 (delta 5), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (5/5), done.
To https://github.com/lschlestein/iniciando-com-git.git
 * [new branch]      develop -> develop
Branch 'develop' set up to track remote branch 'develop' from 'origin'.
```

Obtendo pull mudanças do GitHub (Origin->Develop)
```Terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git pull origin develop
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 947 bytes | 67.00 KiB/s, done.
From https://github.com/lschlestein/iniciando-com-git
 * branch            develop    -> FETCH_HEAD
   d1f45f3..8d66bab  develop    -> origin/develop
Updating d1f45f3..8d66bab
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

git checkout troca as branchs
```terminal
C:\Users\Lucas\Desktop\iniciando-com-git>git checkout master
Switched to branch 'master'

C:\Users\Lucas\Desktop\iniciando-com-git>git merge dev
Updating d2a293e..2af316c
Fast-forward
 .idea/.gitignore            |  8 ++++++++
 .idea/.name                 |  1 +
 .idea/iniciando-com-git.iml |  9 +++++++++
 .idea/misc.xml              |  6 ++++++
 .idea/modules.xml           |  8 ++++++++
 .idea/vcs.xml               |  6 ++++++
 README.md                   |  1 +
 index.html                  | 12 ++++++++----
 script.js                   |  3 +++
 9 files changed, 50 insertions(+), 4 deletions(-)
 create mode 100644 .idea/.gitignore
 create mode 100644 .idea/.name
 create mode 100644 .idea/iniciando-com-git.iml
 create mode 100644 .idea/misc.xml
 create mode 100644 .idea/modules.xml
 create mode 100644 .idea/vcs.xml
 create mode 100644 README.md
```
[Praticando Branchs](https://learngitbranching.js.org/?locale=pt_BR)

Repositórios remotos GitHub, Bitbucket, GitLab Gitness


