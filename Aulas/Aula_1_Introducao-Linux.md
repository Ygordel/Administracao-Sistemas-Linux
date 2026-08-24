# 📘 Aula 01 --- Introdução ao Sistema Operacional Linux

**Curso:** Administração de Sistemas Linux\
**Capítulo:** 1 --- Introdução ao Sistema Operacional Linux\
**Professor:** Ygor Silva

## 🎯 Objetivos da aula

Nesta aula são apresentados os fundamentos necessários para compreender
a organização e a administração de sistemas Linux.

Ao final, o estudante deverá compreender:

-   a arquitetura básica de um sistema Linux;
-   o papel do kernel, shell, bibliotecas e aplicações;
-   o conceito de distribuição Linux;
-   o ciclo de vida e o suporte de uma distribuição;
-   a organização do sistema de arquivos;
-   os principais tipos de arquivos;
-   permissões de arquivos e diretórios;
-   bits especiais: SUID, SGID e Sticky Bit;
-   o conceito básico de ACL.

## 🧩 1. Arquitetura do Linux

A arquitetura do Linux pode ser entendida por diferentes camadas de
software, com o **kernel** ocupando uma posição central entre o hardware
e as aplicações.

### Kernel

O kernel é o núcleo do sistema operacional e atua no gerenciamento dos
recursos computacionais.

Entre suas principais responsabilidades estão:

-   gerenciamento de processos;
-   gerenciamento de memória;
-   gerenciamento de entrada e saída;
-   detecção e interação com dispositivos;
-   manutenção e organização do sistema de arquivos.

### Bibliotecas de funções

As bibliotecas fornecem funções utilizadas pelas aplicações para
solicitar recursos ao sistema operacional, como operações de abertura,
leitura, escrita e fechamento de arquivos.

### Shell

O shell interpreta os comandos digitados pelo usuário e permite
interagir com o sistema por meio de um terminal.

Exemplos citados no material:

-   `sh`
-   `csh`
-   `bash`
-   `ksh`
-   `tcsh`

### Aplicações

São os programas utilizados pelos usuários, como editores de texto,
compiladores, planilhas e outros softwares.

## 🐧 2. Linux Standard Base --- LSB

O **Linux Standard Base (LSB)** busca estabelecer uma base comum para
sistemas Linux, contribuindo para a interoperabilidade entre diferentes
distribuições.

Material de referência apresentado na aula:

https://refspecs.linuxfoundation.org/LSB_5.0.0/allspecs.shtml

## 📦 3. Distribuições Linux

Uma distribuição Linux reúne o kernel, softwares e utilitários
necessários para formar um sistema operacional utilizável.

Exemplos apresentados:

-   Debian
-   Ubuntu
-   Linux Mint
-   Fedora
-   CentOS
-   Red Hat Enterprise Linux
-   SUSE
-   Slackware

## 🔄 4. Ciclo de vida

O ciclo de vida representa o período em que uma distribuição recebe
atualizações, correções e suporte.

É importante verificar as políticas oficiais de cada distribuição antes
de utilizar um sistema em produção.

## 🗂️ 5. Sistema de arquivos --- FHS

O **Filesystem Hierarchy Standard (FHS)** define uma organização
padronizada dos principais diretórios do Linux.

  Diretório   Finalidade
  ----------- -----------------------------------------
  `/`         Diretório raiz
  `/bin`      Comandos essenciais
  `/boot`     Arquivos relacionados à inicialização
  `/dev`      Arquivos de dispositivos
  `/etc`      Arquivos de configuração
  `/home`     Diretórios pessoais dos usuários
  `/lib`      Bibliotecas compartilhadas
  `/media`    Pontos de montagem de mídias removíveis
  `/mnt`      Montagens temporárias
  `/opt`      Softwares adicionais
  `/root`     Diretório pessoal do usuário root
  `/run`      Informações de execução do sistema
  `/sbin`     Comandos administrativos
  `/srv`      Dados disponibilizados por serviços
  `/tmp`      Arquivos temporários
  `/var`      Dados variáveis, como logs e spool

## 💾 6. Inodes

O inode é uma estrutura mantida pelo kernel que armazena informações
relacionadas a um arquivo, como:

-   tipo;
-   proprietário;
-   grupo;
-   permissões;
-   datas;
-   número de links;
-   tamanho;
-   localização dos dados no disco.

Comandos relacionados apresentados na aula:

``` bash
df -i
ls -i
```

## 📄 7. Tipos de arquivos

O Linux trabalha com diferentes tipos de arquivos, incluindo:

-   arquivos regulares;
-   diretórios;
-   arquivos de dispositivos;
-   sockets;
-   named pipes;
-   links simbólicos;
-   hard links.

### Links

**Symbolic link:** funciona como uma referência por nome para outro
arquivo ou diretório.

``` bash
ln -s arquivo destino
```

**Hard link:** associa outro nome ao mesmo inode.

``` bash
ln arquivo destino
```

## 🔐 8. Permissões

As permissões tradicionais do Linux controlam três categorias:

-   **usuário/dono (u)**
-   **grupo (g)**
-   **outros (o)**

E três operações:

-   `r` --- leitura;
-   `w` --- escrita;
-   `x` --- execução.

### chmod

O comando `chmod` altera permissões de arquivos e diretórios.

Exemplo:

``` bash
chmod 540 arquivo
chmod 775 diretorio
```

## ⚙️ 9. Bits especiais

A aula apresenta três mecanismos especiais:

### SUID

Representado por `s` e relacionado à execução de determinados arquivos
com os privilégios do proprietário.

### SGID

Representado por `s` e utilizado em arquivos executáveis e diretórios,
conforme o contexto.

### Sticky Bit

Representado por `t` e utilizado principalmente em diretórios
compartilhados para controlar a remoção de arquivos.

Exemplos:

``` bash
chmod 1775 diretorio
chmod 2775 diretorio
```

## 🛡️ 10. ACL

As **Access Control Lists (ACLs)** ampliam o modelo tradicional de
permissões do Linux, permitindo definir permissões adicionais para
usuários e grupos.

Comandos apresentados:

``` bash
getfacl arquivo
setfacl -m g:grupo:r arquivo
```

## 🧪 Prática da Aula 01

A aplicação prática dos conceitos está organizada em um arquivo
separado:

**📄 Tarefa 01 --- Administração de Sistemas Linux**

A atividade trabalha principalmente:

-   criação de diretórios;
-   redirecionamento de saída;
-   permissões;
-   `find`;
-   SUID;
-   SGID;
-   alteração de grupo;
-   compactação com `tar`.

------------------------------------------------------------------------

### 📚 Material de referência

-   Linux Standard Base:
    https://refspecs.linuxfoundation.org/LSB_5.0.0/allspecs.shtml
-   Filesystem Hierarchy Standard:
    https://wiki.linuxfoundation.org/lsb/fhs
-   Ubuntu --- ciclo de vida:
    https://www.ubuntu.com/info/release-end-of-life

> **Observação:** este README é uma síntese didática da Aula 01. Para a
> atividade prática, consulte o arquivo **Tarefa01.pdf** disponibilizado
> neste repositório.
