# 📝 Tarefa 01 --- Administração de Sistemas Linux

**Capítulo:** 1 --- Introdução ao Sistema Operacional Linux\
**Professor:** Ygor Silva

## 🎯 Objetivo

Aplicar, em uma máquina virtual Linux, conceitos básicos de
administração de sistemas, incluindo diretórios, arquivos,
redirecionamento, permissões, `find`, SUID, SGID, grupos e compactação
com `tar`.

## 📌 Atividades

Acesse a máquina virtual Linux utilizando a conta do usuário `aluno`.

### 1. Criar o diretório da atividade

No diretório pessoal do usuário, crie:

``` bash
capitulo1
```

### 2. Criar o arquivo e redirecionar a data

Dentro de `capitulo1`, crie `atividade1.txt` e grave nele a saída do
comando `date`.

Exemplo:

``` bash
date > ~/capitulo1/atividade1.txt
```

### 3. Configurar as permissões

O arquivo `atividade1.txt` deverá possuir:

-   **Dono:** leitura, escrita e execução;
-   **Grupo:** nenhuma permissão;
-   **Outros:** nenhuma permissão.

A representação octal correspondente é:

``` text
700
```

Comando:

``` bash
chmod 700 ~/capitulo1/atividade1.txt
```

Verificação:

``` bash
ls -l ~/capitulo1/atividade1.txt
```

### 4. Criar o diretório para os arquivos copiados

``` bash
mkdir ~/capitulo1/arquivosCopiados
```

### 5. Localizar um arquivo com SUID

Utilize `find` dentro de `/usr/bin` para localizar um arquivo com o bit
**SUID** ativado.

Exemplo de consulta:

``` bash
find /usr/bin -type f -perm -4000 -print
```

Escolha um dos resultados e copie-o para:

``` text
~/capitulo1/arquivosCopiados/
```

Exemplo:

``` bash
cp /usr/bin/ARQUIVO_ESCOLHIDO ~/capitulo1/arquivosCopiados/
```

### 6. Localizar um arquivo com SGID

Utilize `find` para localizar um arquivo com o bit **SGID** ativado:

``` bash
find /usr/bin -type f -perm -2000 -print
```

Escolha um resultado e copie-o para:

``` text
~/capitulo1/arquivosCopiados/
```

Exemplo:

``` bash
cp /usr/bin/ARQUIVO_ESCOLHIDO ~/capitulo1/arquivosCopiados/
```

### 7. Alterar o grupo recursivamente

Altere o grupo do diretório `arquivosCopiados` e de seu conteúdo para:

``` text
adm
```

Comando:

``` bash
chgrp -R adm ~/capitulo1/arquivosCopiados
```

Verificação:

``` bash
ls -l ~/capitulo1/arquivosCopiados
```

### 8. Criar o pacote da atividade

Compacte o diretório `capitulo1` utilizando `tar`.

Exemplo:

``` bash
tar -cvf capitulo1.tar ~/capitulo1
```

Para gerar um pacote compactado em gzip:

``` bash
tar -czvf capitulo1.tar.gz ~/capitulo1
```

## ✅ Conferência final

Antes de enviar a atividade, verifique:

``` bash
ls -l ~/capitulo1
ls -l ~/capitulo1/arquivosCopiados
ls -l ~/capitulo1/atividade1.txt
```

Também é possível verificar permissões especiais com:

``` bash
ls -l ~/capitulo1/arquivosCopiados
```

## 📦 Entrega

O resultado solicitado na atividade é um pacote contendo o diretório:

``` text
capitulo1/
├── atividade1.txt
└── arquivosCopiados/
    ├── arquivo-com-SUID
    └── arquivo-com-SGID
```

O pacote `capitulo1.tar` ou `capitulo1.tar.gz` deverá ser enviado como
resultado da atividade.

## 📚 Referências indicadas na atividade

### Redirecionamento de entrada e saída

https://www.ppgia.pucpr.br/pt/arquivos/techdocs/linux/foca-iniciante/ch-redir.html

### Comando find --- SUID e SGID

https://www.tecmint.com/how-to-find-files-with-suid-and-sgid-permissions-in-linux/

### Comando tar

https://guialinux.uniriotec.br/tar/

https://www.binarytides.com/linux-tar-command/

------------------------------------------------------------------------

**Professor: Ygor Silva**\
*Administração de Sistemas Linux --- Capítulo 1*
