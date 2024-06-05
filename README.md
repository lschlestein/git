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


