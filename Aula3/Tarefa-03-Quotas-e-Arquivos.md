# 📘 Tarefa 3 — Gerenciamento de Discos e Sistema de Arquivos

**Professor:** Ygor Silva  
**Curso:** Administração de Sistemas Linux  
**Atividade:** Tarefa 3  
**Tema:** Particionamento, Sistema de Arquivos e Gerenciamento de Armazenamento

---

## 🎯 Objetivo

Praticar o gerenciamento de dispositivos de armazenamento no Linux, realizando a identificação de um novo disco, criação de uma partição, formatação com o sistema de arquivos **ext4**, montagem do dispositivo e consulta das informações de espaço e inodes.

---

# 💽 1. Adicionando um novo disco

Para iniciar a atividade, adicione um novo disco virtual de **8 GB** à máquina virtual utilizada no laboratório.

Depois de adicionar o disco, é necessário identificar qual dispositivo foi associado ao sistema.

Algumas ferramentas que podem ser utilizadas:

```bash

lsblk
sudo fdisk -l
sudo parted -l

Também é possível utilizar:

sudo lshw

ou consultar mensagens do kernel:

dmesg | grep -E "/dev/sd[a-z]"

Um exemplo de identificação seria:

/dev/sdb

⚠️ Atenção: confirme cuidadosamente o dispositivo antes de executar qualquer comando de particionamento ou formatação.

🧱 2. Criando a tabela de partições

Nesta atividade será utilizada uma tabela de partições do tipo MBR (msdos).

Para abrir o disco no fdisk:

sudo fdisk /dev/sdb

Dentro do fdisk, utilize:

o

A opção o cria uma nova tabela de partições DOS/MBR.

Em seguida, crie uma nova partição:

n

Escolha:

p

para criar uma partição primária.

Utilize:

1

para definir a primeira partição.

Para utilizar todo o espaço disponível, aceite os valores padrão de primeiro e último setor.

Finalmente:

w

para gravar as alterações no disco.

🔎 3. Conferindo a partição

Depois de criar a partição, confira o resultado:

lsblk

ou:

sudo fdisk -l /dev/sdb

O resultado deverá apresentar uma estrutura semelhante a:

/dev/sdb
└─/dev/sdb1

A partição criada será:

/dev/sdb1
🗃️ 4. Criando o sistema de arquivos ext4

Formate a nova partição utilizando o sistema de arquivos ext4:

sudo mkfs.ext4 /dev/sdb1

Após a formatação, confira as informações:

sudo blkid /dev/sdb1

O sistema deverá apresentar informações semelhantes a:

/dev/sdb1: UUID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" TYPE="ext4"
📂 5. Criando o ponto de montagem

Crie o diretório que será utilizado como ponto de montagem:

sudo mkdir -p /mnt

Caso o diretório /mnt já exista, não é necessário criá-lo novamente.

🔗 6. Montando a partição

Monte a partição:

sudo mount /dev/sdb1 /mnt

Verifique se o dispositivo foi montado:

mount | grep /mnt

Também é possível utilizar:

df -h
📊 7. Consultando o espaço utilizado

Utilize o comando df para verificar o espaço disponível e utilizado:

df -h /mnt

O parâmetro -h apresenta os valores em formato mais fácil de interpretar.

Exemplo:

Filesystem      Size  Used Avail Use% Mounted on
/dev/sdb1       7.8G   ...  ...   ...  /mnt
🧩 8. Consultando os inodes

Para consultar a quantidade de inodes utilizados e disponíveis:

df -i /mnt

O resultado apresentará informações semelhantes a:

Filesystem      Inodes IUsed IFree IUse% Mounted on
/dev/sdb1        ...    ...   ...    ...  /mnt
Conceito

Inodes armazenam informações sobre arquivos e diretórios, incluindo metadados e referências aos blocos utilizados pelo sistema de arquivos.

📁 9. Consultando a utilização do diretório

O comando du permite verificar o espaço ocupado pelos arquivos e diretórios.

Execute:

du -sh /mnt

Para visualizar os diretórios existentes:

du -h /mnt
🔍 10. Identificando o dispositivo

Utilize:

lsblk -f

Esse comando apresenta informações como:

dispositivo;
sistema de arquivos;
LABEL;
UUID;
ponto de montagem.

Exemplo:

NAME   FSTYPE LABEL UUID                                 MOUNTPOINT
sdb
└─sdb1 ext4         xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx /mnt
🏷️ 11. Consultando o UUID

Outra forma de consultar o UUID:

sudo blkid /dev/sdb1

O UUID pode ser utilizado para identificar o dispositivo no arquivo:

/etc/fstab
🧪 12. Teste prático

Para confirmar que a partição está funcionando, crie um arquivo de teste:

sudo touch /mnt/teste.txt

Confira:

ls -l /mnt

Crie também um diretório:

sudo mkdir /mnt/laboratorio

Verifique:

ls -la /mnt
📊 13. Verificação final

Execute os comandos abaixo:

lsblk
lsblk -f
df -h /mnt
df -i /mnt
sudo blkid /dev/sdb1
du -sh /mnt
✅ Checklist da Tarefa 3
 Adicionar disco virtual de 8 GB.
 Identificar o novo dispositivo.
 Criar tabela de partições MBR.
 Criar uma partição primária.
 Utilizar todo o espaço disponível.
 Criar o sistema de arquivos ext4.
 Criar o ponto de montagem /mnt.
 Montar a partição.
 Verificar o espaço disponível.
 Verificar o espaço utilizado.
 Verificar os inodes.
 Consultar o UUID.
 Criar arquivo de teste.
 Criar diretório de laboratório.
 Realizar a verificação final.
🧠 Comandos utilizados
Comando	Finalidade
lsblk	Lista dispositivos de bloco
fdisk	Gerencia partições
parted	Gerencia tabelas e partições
lshw	Exibe informações de hardware
dmesg	Consulta mensagens do kernel
mkfs.ext4	Cria um sistema de arquivos ext4
mount	Monta um sistema de arquivos
umount	Desmonta um sistema de arquivos
df	Consulta espaço utilizado e disponível
df -i	Consulta utilização de inodes
du	Consulta espaço utilizado por arquivos/diretórios
blkid	Exibe UUID e tipo do sistema de arquivos
lsblk -f	Exibe informações detalhadas dos filesystems
📸 Evidências sugeridas

Para documentar a atividade no GitHub, recomenda-se registrar capturas de tela dos seguintes momentos:

Disco de 8 GB adicionado à máquina virtual.
Identificação do novo dispositivo com lsblk.
Criação da tabela MBR.
Criação da partição /dev/sdb1.
Formatação com mkfs.ext4.
Montagem em /mnt.
Resultado do df -h.
Resultado do df -i.
Resultado do lsblk -f.
Arquivo e diretório criados no ponto de montagem.
📌 Resultado esperado

Ao final da atividade, deverá existir um novo disco virtual de aproximadamente 8 GB, contendo uma partição primária formatada com ext4 e montada no diretório:

/mnt

A partição deverá estar acessível pelo sistema e apresentar informações de espaço e inodes por meio dos comandos:

df -h /mnt

e:

df -i /mnt
👨‍🏫 Professor

Ygor Silva

📚 Curso

Administração de Sistemas Linux

📝 Atividade

Tarefa 3 — Particionamento e Sistema de Arquivos

⭐ Material organizado para estudo, prática em laboratório e registro das atividades no GitHub.
