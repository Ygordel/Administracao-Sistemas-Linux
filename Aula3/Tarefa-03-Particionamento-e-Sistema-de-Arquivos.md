# 📘 Tarefa 3 — Particionamento e Sistema de Arquivos

**Professor:** Ygor Silva  
**Curso:** Administração de Sistemas Linux  
**Atividade:** Tarefa 3  
**Tema:** Particionamento, Sistema de Arquivos e Gerenciamento de Armazenamento

---

## 🎯 Objetivo

Praticar o gerenciamento de dispositivos de armazenamento no Linux, realizando a identificação de um novo disco, criação de uma partição, formatação com o sistema de arquivos **ext4**, montagem do dispositivo e consulta das informações de espaço e inodes.

---

## 💽 1. Adicionando um novo disco

Para iniciar a atividade, adicione um novo disco virtual de **8 GB** à máquina virtual utilizada no laboratório.

Depois de adicionar o disco, identifique qual dispositivo foi associado ao sistema.

### Comandos para identificação

```bash
lsblk
sudo fdisk -l
sudo parted -l
```

Também podem ser utilizados:

```bash
sudo lshw
```

```bash
dmesg | grep -E "/dev/sd[a-z]"
```

Um exemplo de identificação seria:

```text
/dev/sdb
```

> ⚠️ **Atenção:** confirme cuidadosamente o dispositivo antes de executar comandos de particionamento ou formatação.

---

## 🧱 2. Criando a tabela de partições

Nesta atividade será utilizada uma tabela de partições do tipo **MBR (msdos)**.

Abra o disco no `fdisk`:

```bash
sudo fdisk /dev/sdb
```

Dentro do `fdisk`, utilize:

```text
o
```

A opção `o` cria uma nova tabela de partições DOS/MBR.

---

## 🧩 3. Criando a partição primária

Dentro do `fdisk`, utilize:

```text
n
```

Escolha:

```text
p
```

para criar uma partição primária.

Depois:

```text
1
```

para utilizar a primeira partição.

Aceite os valores padrão de primeiro e último setor para utilizar todo o espaço disponível.

Grave as alterações:

```text
w
```

---

## 🔎 4. Conferindo a partição

Depois de criar a partição:

```bash
lsblk
```

ou:

```bash
sudo fdisk -l /dev/sdb
```

A estrutura esperada será semelhante a:

```text
/dev/sdb
└── /dev/sdb1
```

---

## 🗃️ 5. Criando o sistema de arquivos ext4

Formate a nova partição utilizando **ext4**:

```bash
sudo mkfs.ext4 /dev/sdb1
```

Confira as informações:

```bash
sudo blkid /dev/sdb1
```

O resultado deverá apresentar o tipo:

```text
TYPE="ext4"
```

> ⚠️ **Atenção:** a formatação pode apagar dados existentes no dispositivo. Execute somente no disco destinado ao laboratório.

---

## 📂 6. Criando o ponto de montagem

Utilize o diretório `/mnt` como ponto de montagem.

Verifique se ele existe:

```bash
ls -ld /mnt
```

Caso necessário:

```bash
sudo mkdir -p /mnt
```

---

## 🔗 7. Montando a partição

Monte a partição:

```bash
sudo mount /dev/sdb1 /mnt
```

Verifique a montagem:

```bash
mount | grep /mnt
```

Também pode ser utilizado:

```bash
df -h /mnt
```

---

## 📊 8. Consultando espaço utilizado e disponível

Utilize:

```bash
df -h /mnt
```

O parâmetro `-h` apresenta os valores em formato legível.

Exemplo:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sdb1       7.8G   ...  ...   ...  /mnt
```

---

## 🧩 9. Consultando inodes

Para verificar os inodes:

```bash
df -i /mnt
```

O resultado apresentará informações semelhantes a:

```text
Filesystem      Inodes IUsed IFree IUse% Mounted on
/dev/sdb1        ...    ...   ...    ...  /mnt
```

### Conceito

Os **inodes** armazenam informações sobre arquivos e diretórios, incluindo metadados e referências aos blocos utilizados pelo sistema de arquivos.

---

## 📁 10. Consultando a utilização do diretório

O comando `du` permite verificar o espaço ocupado pelos arquivos e diretórios.

```bash
du -sh /mnt
```

Para visualizar o conteúdo:

```bash
du -h /mnt
```

---

## 🔍 11. Identificando o sistema de arquivos

Utilize:

```bash
lsblk -f
```

Esse comando apresenta informações como:

- dispositivo;
- sistema de arquivos;
- LABEL;
- UUID;
- ponto de montagem.

Exemplo:

```text
NAME   FSTYPE LABEL UUID                                 MOUNTPOINT
sdb
└─sdb1 ext4         xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx /mnt
```

---

## 🏷️ 12. Consultando o UUID

Utilize:

```bash
sudo blkid /dev/sdb1
```

O UUID identifica exclusivamente o sistema de arquivos e pode ser utilizado no arquivo:

```text
/etc/fstab
```

---

## 🧪 13. Testando a partição

Crie um arquivo de teste:

```bash
sudo touch /mnt/teste.txt
```

Confira:

```bash
ls -l /mnt
```

Crie também um diretório:

```bash
sudo mkdir /mnt/laboratorio
```

Verifique:

```bash
ls -la /mnt
```

---

## 📋 14. Verificação final

Execute os principais comandos:

```bash
lsblk
```

```bash
lsblk -f
```

```bash
df -h /mnt
```

```bash
df -i /mnt
```

```bash
sudo blkid /dev/sdb1
```

```bash
du -sh /mnt
```

---

## 📸 15. Evidências sugeridas

Registre capturas de tela dos principais momentos da atividade:

1. Disco virtual de 8 GB adicionado à máquina virtual.
2. Identificação do novo disco com `lsblk`.
3. Criação da tabela de partições MBR.
4. Criação da partição `/dev/sdb1`.
5. Formatação com `mkfs.ext4`.
6. Montagem da partição em `/mnt`.
7. Resultado do `df -h`.
8. Resultado do `df -i`.
9. Resultado do `lsblk -f`.
10. Arquivo e diretório criados no ponto de montagem.

---

## ✅ Checklist da Tarefa 3

- [ ] Disco virtual de 8 GB adicionado.
- [ ] Novo disco identificado.
- [ ] Tabela de partições MBR criada.
- [ ] Partição primária criada.
- [ ] Espaço disponível utilizado.
- [ ] Sistema de arquivos ext4 criado.
- [ ] Ponto de montagem `/mnt` preparado.
- [ ] Partição montada.
- [ ] Espaço disponível verificado.
- [ ] Inodes verificados.
- [ ] UUID consultado.
- [ ] Arquivo de teste criado.
- [ ] Diretório de laboratório criado.
- [ ] Verificação final realizada.

---

## 🧠 Principais comandos

| Comando | Finalidade |
|---|---|
| `lsblk` | Lista dispositivos de bloco |
| `fdisk` | Gerencia partições |
| `parted` | Gerencia tabelas e partições |
| `lshw` | Exibe informações de hardware |
| `dmesg` | Consulta mensagens do kernel |
| `mkfs.ext4` | Cria sistema de arquivos ext4 |
| `mount` | Monta um sistema de arquivos |
| `umount` | Desmonta um sistema de arquivos |
| `df` | Consulta espaço utilizado e disponível |
| `df -i` | Consulta utilização de inodes |
| `du` | Consulta espaço utilizado |
| `blkid` | Exibe UUID e tipo do filesystem |
| `lsblk -f` | Exibe informações dos sistemas de arquivos |

---

## 📌 Resultado esperado

Ao final da atividade, deverá existir um disco virtual de aproximadamente **8 GB**, contendo uma partição primária formatada com **ext4** e montada no diretório:

```text
/mnt
```

A partição deverá estar acessível pelo sistema e apresentar informações de espaço e inodes por meio dos comandos:

```bash
df -h /mnt
```

```bash
df -i /mnt
```

---

## 👨‍🏫 Professor

**Ygor Silva**

## 📚 Curso

**Administração de Sistemas Linux**

## 📝 Atividade

**Tarefa 3 — Particionamento e Sistema de Arquivos**

---

⭐ Material organizado para estudo, prática em laboratório e registro das atividades no GitHub.
