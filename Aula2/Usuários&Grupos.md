# 👥 Gerenciamento de Usuários e Grupos no Linux

**Professor:** Ygor Silva  
**Curso:** Administração de Sistemas Linux  
**Tema:** Gerenciamento de Usuários e Grupos  
**Ambiente:** Linux / Debian

---

## 📚 Sobre a Aula

Esta aula apresenta os principais conceitos e procedimentos utilizados no **gerenciamento de usuários e grupos em sistemas Linux**.

Durante a prática são apresentados métodos de administração utilizando comandos do sistema e, quando necessário, a edição dos principais arquivos de configuração relacionados a usuários, grupos, senhas e políticas de autenticação.

---

## 🎯 Objetivos

Ao finalizar esta atividade, o aluno deverá ser capaz de:

- Criar e excluir usuários;
- Criar e excluir grupos;
- Compreender UID e GID;
- Configurar grupos primários e secundários;
- Gerenciar senhas;
- Bloquear e desbloquear contas;
- Alterar o shell de usuários;
- Configurar validade de senhas;
- Administrar diretórios `HOME`;
- Criar usuários em lote;
- Alterar senhas em lote;
- Identificar os principais arquivos de usuários e grupos.

---

# 📂 Principais Arquivos do Linux

Os principais arquivos relacionados ao gerenciamento de usuários e grupos são:

```text
/etc/passwd
/etc/shadow
/etc/group
/etc/gshadow
/etc/skel
/etc/login.defs
/etc/passwd

Arquivo que contém informações básicas das contas dos usuários.

Exemplo:

aluno:x:1000:1000:Aluno ESR:/home/aluno:/bin/bash

Edição utilizando:

vipw
/etc/shadow

Arquivo utilizado para armazenar informações relacionadas às senhas e políticas de expiração.

Edição utilizando:

vipw -s

Exemplo:

aluno:!::0:60:7:::
/etc/group

Arquivo responsável pelas informações dos grupos existentes no sistema.

Edição utilizando:

vigr

Exemplo:

aluno:x:1000:
/etc/gshadow

Arquivo relacionado às informações de segurança dos grupos.

Edição utilizando:

vigr -s

Exemplo:

aluno:!::
/etc/skel

Diretório utilizado como modelo para criação dos diretórios HOME dos novos usuários.

/etc/login.defs

Arquivo que contém configurações e políticas utilizadas pelo sistema para criação e gerenciamento de usuários e senhas.

👥 1. Gerenciamento de Grupos
1.1 Criando um grupo

Informações utilizadas no laboratório:

Configuração	Valor
Nome do grupo	aluno
GID	1000

Criar o grupo utilizando o comando:

groupadd -g 1000 aluno
1.2 Criando o grupo manualmente

Editar o arquivo /etc/group:

vigr

Adicionar:

aluno:x:1000:

O campo x representa a utilização do mecanismo de shadow passwords.

Editar o arquivo /etc/gshadow:

vigr -s

Adicionar:

aluno:!::
🛠️ 2. Comandos para Gerenciamento de Grupos
Definir senha para um grupo
gpasswd coordenadores
Tornar um usuário administrador do grupo
gpasswd -A joao vendas
Adicionar usuário ao grupo
usermod -a -G contabilidade joao

Outra possibilidade:

gpasswd -a joao contabilidade
Remover usuário do grupo
gpasswd -d maria vendas
Excluir grupo
groupdel estagiarios
👤 3. Gerenciamento de Usuários
3.1 Informações da conta
Configuração	Valor
Nome	Aluno ESR
Usuário	aluno
UID	1000
GID	1000
Grupo primário	aluno
Diretório HOME	/home/aluno
Shell	/bin/bash
Validade da senha	60 dias
Aviso de expiração	7 dias
Mínimo para alteração	0 dias
4. Criando um Usuário
4.1 Utilizando o comando useradd

Criar a conta:

useradd -m -s /bin/bash -u 1000 -g 1000 -c "Aluno ESR" -d /home/aluno -K PASS_MAX_DAYS=60 -K PASS_MIN_DAYS=0 -K PASS_WARN_AGE=7 aluno

Definir a senha:

passwd aluno
5. Criando o Usuário Manualmente

Editar o arquivo /etc/passwd:

vipw

Adicionar:

aluno:x:1000:1000:Aluno ESR:/home/aluno:/bin/bash

Editar o arquivo /etc/shadow:

vipw -s

Adicionar:

aluno:!::0:60:7:::

Definir a senha:

passwd aluno
🏠 6. Configuração do Diretório HOME

Criar o diretório:

mkdir /home/aluno

Copiar os arquivos do /etc/skel:

cp -r /etc/skel/.[a-zA-Z0-9]* /home/aluno
cp -r /etc/skel/* /home/aluno

Alterar o proprietário:

chown -R aluno /home/aluno

Alterar o grupo:

chgrp -R aluno /home/aluno

Configurar as permissões:

chmod 750 /home/aluno
🔐 7. Gerenciamento de Senhas
Alterar senha
passwd maria
Definir validade da senha

Exemplo: 120 dias.

passwd -x 120 joao
Bloquear usuário
passwd -l aluno
Desbloquear usuário
passwd -u aluno
👨‍💻 8. Alteração de Shell

Alterar o shell da usuária maria:

chsh -s /bin/sh maria

Exemplo utilizando Bash:

chsh -s /bin/bash maria
👥 9. Gerenciamento de Grupos dos Usuários

Adicionar o usuário joao ao grupo vendas:

usermod -a -G vendas joao

Alterar o grupo primário do usuário:

usermod -g users joao
🗑️ 10. Exclusão de Usuários

Excluir somente a conta:

userdel marcos

Excluir a conta e seu diretório HOME:

userdel -r marcos
📦 11. Criação de Usuários em Lote

O comando newusers permite criar ou atualizar várias contas de usuários utilizando um único arquivo.

Criar o arquivo:

cat contas.txt

Exemplo:

conta1:senha1:2000:100:Nome Conta 1:/home/conta1:/bin/bash
conta2:senha2:2001:100:Nome Conta 2:/home/conta2:/bin/bash
conta3:senha3:2002:100:Nome Conta 3:/home/conta3:/bin/bash
conta4:senha4:2003:100:Nome Conta 4:/home/conta4:/bin/bash

Criar as contas:

newusers ./contas.txt
🔄 12. Alteração de Senhas em Lote

O comando chpasswd permite alterar as senhas de vários usuários.

Executar:

chpasswd

Formato:

nome_usuario:senha

Criar um arquivo:

cat senhas.txt

Exemplo:

joao:senha123
maria:senha123
jose:senha123
marcos:senha123
felipe:senha123

Aplicar as alterações utilizando SHA-512:

cat senhas.txt | chpasswd -c SHA512
🛠️ 13. Principais Comandos
Comando	Função
useradd	Criar usuário
usermod	Alterar configurações do usuário
userdel	Excluir usuário
passwd	Gerenciar senhas
chsh	Alterar shell
groupadd	Criar grupo
groupdel	Excluir grupo
gpasswd	Administrar grupos
newusers	Criar/atualizar usuários em lote
chpasswd	Alterar senhas em lote
vigr	Editar /etc/group
vigr -s	Editar /etc/gshadow
vipw	Editar /etc/passwd
vipw -s	Editar /etc/shadow
🔎 14. Resumo UID e GID
UID

UID — User ID

Identificador numérico utilizado pelo Linux para identificar cada usuário.

Exemplo:

UID = 1000
GID

GID — Group ID

Identificador numérico utilizado pelo Linux para identificar um grupo.

Exemplo:

GID = 1000
🧪 15. Atividade Prática

Realizar as seguintes tarefas:

Criar o grupo aluno;
Utilizar o GID 1000;
Criar o usuário aluno;
Utilizar o UID 1000;
Configurar o grupo primário;
Criar /home/aluno;
Configurar /bin/bash;
Definir uma senha;
Configurar validade da senha para 60 dias;
Configurar aviso de expiração para 7 dias;
Adicionar o usuário a um grupo secundário;
Alterar o grupo primário;
Bloquear a conta;
Desbloquear a conta;
Criar usuários utilizando newusers;
Alterar senhas utilizando chpasswd;
Testar o login dos usuários criados.
✅ 16. Checklist da Prática
[ ] Grupo criado
[ ] GID configurado
[ ] Usuário criado
[ ] UID configurado
[ ] Grupo primário configurado
[ ] Diretório HOME criado
[ ] Shell configurado
[ ] Senha definida
[ ] Validade da senha configurada
[ ] Usuário adicionado ao grupo secundário
[ ] Conta bloqueada
[ ] Conta desbloqueada
[ ] Usuários em lote criados
[ ] Senhas em lote configuradas
[ ] Login testado
📌 Conclusão

O gerenciamento de usuários e grupos é uma das atividades fundamentais da Administração de Sistemas Linux.

A utilização correta de comandos como useradd, usermod, userdel, passwd, groupadd, groupdel, gpasswd, newusers e chpasswd permite administrar contas, grupos, senhas e políticas de acesso de forma organizada.

Os arquivos /etc/passwd, /etc/shadow, /etc/group e /etc/gshadow também são fundamentais para compreender como o Linux organiza as informações relacionadas às contas e grupos.

👨‍🏫 Professor

Ygor Silva

Curso: Administração de Sistemas Linux

📌 Material desenvolvido para fins de estudo, prática, laboratório e documentação no GitHub.

⭐ Continue praticando, documentando e evoluindo seus conhecimentos em Linux!
