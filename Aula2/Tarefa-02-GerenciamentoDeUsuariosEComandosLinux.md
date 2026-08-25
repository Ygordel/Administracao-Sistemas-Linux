📘 Tarefa 02 — Administração de Sistemas Linux

Professor: Ygor Silva
Curso: Administração de Sistemas Linux
Atividade: Tarefa 02
Ambiente: Linux / Máquina Virtual

A atividade trabalha useradd, criação de usuários, configuração de diretório HOME, grupo sudo, redirecionamento de saída, gerenciamento de sessões e compactação do diretório /home utilizando tar.

# 🐧 Tarefa 02 — Administração de Sistemas Linux

**Professor:** Ygor Silva  
**Curso:** Administração de Sistemas Linux  
**Atividade:** Tarefa 02  
**Ambiente:** Linux / Máquina Virtual

---

## 📚 Sobre a Tarefa

A Tarefa 02 apresenta atividades práticas de administração de usuários,
grupos, diretórios, permissões, redirecionamento de saída e compactação
de arquivos no Linux.

As atividades iniciais podem ser executadas utilizando a conta `aluno`
com o comando `sudo` ou diretamente utilizando a conta `root`.

---

# 🎯 Objetivos

- Configurar o ambiente para criação de usuários;
- Utilizar o comando `useradd`;
- Configurar diretórios `HOME`;
- Criar subdiretórios automaticamente;
- Criar usuários no Linux;
- Configurar senhas e shell;
- Adicionar usuários ao grupo `sudo`;
- Utilizar redirecionamento de saída;
- Trabalhar com o comando `groups`;
- Encerrar e iniciar sessões de usuários;
- Utilizar o comando `tar`;
- Criar um pacote contendo o diretório `/home`.

---

# 👤 1. Configuração do `useradd`

Configurar o ambiente para que todo usuário criado pelo comando
`useradd` possua automaticamente o subdiretório:

```text
/home/USUARIO/atividades

Exemplo:

/home/joao/atividades

A configuração deve fazer com que o diretório atividades seja criado
automaticamente dentro do HOME de cada novo usuário.

👨‍💻 2. Criar um Usuário

Cadastrar um usuário utilizando seu próprio nome.

O usuário deverá possuir:

Nome de usuário;
Senha segura;
Diretório HOME;
Shell de preferência.

A criação do diretório HOME e a configuração do shell podem ser
realizadas diretamente pelo useradd ou posteriormente.

Exemplo:

sudo useradd -m -s /bin/bash usuario

Definir a senha:

sudo passwd usuario

Verificar as informações da conta:

id usuario
👥 3. Adicionar o Usuário ao Grupo sudo

Adicionar o usuário criado ao grupo sudo:

sudo usermod -a -G sudo usuario

Verificar os grupos:

groups usuario

ou:

id usuario
🔐 4. Acessar o Usuário Criado

Acessar o sistema utilizando o usuário criado na atividade anterior.

Exemplo:

su - usuario

Ou realizar um novo login utilizando a conta criada.

📄 5. Redirecionamento do Comando groups

Executar o comando:

groups

Redirecionar a saída para o arquivo:

~/atividades/meus-grupos.txt

Comando:

groups > ~/atividades/meus-grupos.txt

Verificar o conteúdo:

cat ~/atividades/meus-grupos.txt
🔄 6. Encerrar as Sessões

Encerrar todas as sessões abertas no Linux.

Exemplos de usuários que podem estar conectados:

aluno
aluno2
usuario

Depois de encerrar as sessões, realizar um novo login utilizando o
usuário criado na atividade 2.

📦 7. Compactação do Diretório /home

Utilizar o comando tar para criar um pacote contendo o diretório
/home da máquina virtual.

Como será necessário acessar arquivos e diretórios que podem exigir
privilégios administrativos, utilizar sudo.

Exemplo:

sudo tar -cvf home.tar /home

Para gerar um arquivo compactado com gzip:

sudo tar -czvf home.tar.gz /home

Verificar o arquivo criado:

ls -lh home.tar.gz
🔎 8. Verificação

Verificar o conteúdo do pacote:

tar -tzf home.tar.gz

O conteúdo deverá apresentar os diretórios existentes em:

/home
✅ Checklist da Tarefa
[ ] Configurar o useradd
[ ] Criar automaticamente o diretório atividades
[ ] Criar usuário
[ ] Definir senha segura
[ ] Configurar diretório HOME
[ ] Configurar shell
[ ] Adicionar usuário ao grupo sudo
[ ] Executar o comando groups
[ ] Criar meus-grupos.txt
[ ] Encerrar as sessões existentes
[ ] Realizar novo login
[ ] Criar pacote do diretório /home
[ ] Utilizar sudo no comando tar
[ ] Verificar o arquivo gerado
🧠 Comandos Utilizados
Comando	Função
useradd	Criar usuário
passwd	Definir ou alterar senha
usermod	Alterar configurações do usuário
groups	Exibir grupos do usuário
id	Exibir UID, GID e grupos
su	Alternar usuário
cat	Exibir conteúdo de arquivos
sudo	Executar comandos com privilégios
tar	Criar e manipular arquivos compactados
ls	Listar arquivos e diretórios
📚 Referências da Atividade
Sudo
Guia Foca — Uso do comando sudo
Ubuntu/Kubuntu — Root e Sudo
Redirecionamento
Guia Foca — Redirecionamento de entrada e saída
Tar
Guia Linux — Comando tar
BinaryTides — Linux tar Command
👨‍🏫 Professor

Ygor Silva

📌 Material organizado para estudo, prática, laboratório e documentação no GitHub.

⭐ Continue praticando e documentando sua evolução em Linux!
