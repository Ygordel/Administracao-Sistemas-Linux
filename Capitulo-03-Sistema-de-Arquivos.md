# 🐧 Administração de Sistemas Linux

## Capítulo 03 --- Sistema de Arquivos

> **Professor:** Ygor Silva\
> **Curso:** Administração de Sistemas Linux\
> **Tema:** Gerenciamento de discos, sistemas de arquivos, LVM e quotas

------------------------------------------------------------------------

## 📚 Sobre o capítulo

Este capítulo apresenta os principais conceitos e procedimentos
relacionados ao armazenamento no Linux. São abordados particionamento de
discos, estruturas MBR e GPT, gerenciamento de volumes lógicos com LVM,
sistemas de arquivos, montagem de dispositivos e controle de utilização
de espaço por meio de quotas.

A documentação foi organizada para servir como material de consulta e
apoio às atividades práticas realizadas em laboratório.

------------------------------------------------------------------------

## 🎯 Objetivos

Ao finalizar o capítulo, o aluno deverá ser capaz de:

-   compreender as estruturas de particionamento **MBR** e **GPT**;
-   identificar as vantagens do particionamento;
-   compreender o funcionamento do **LVM**;
-   criar e gerenciar partições;
-   criar sistemas de arquivos;
-   utilizar `mkfs`, `fsck`, `mount`, `umount`, `du` e `df`;
-   compreender e utilizar o arquivo `/etc/fstab`;
-   identificar dispositivos por **LABEL** e **UUID**;
-   compreender blocos e inodes;
-   administrar quotas de usuários e grupos;
-   verificar e gerenciar a utilização de espaço em disco.

------------------------------------------------------------------------

# 1. 💽 Estrutura dos discos

No Linux, um disco pode ser dividido em uma ou mais partições. Cada
partição pode receber um sistema de arquivos compatível com o sistema
operacional.

As partições são integradas a uma única árvore de diretórios. O
diretório raiz `/` é o ponto principal dessa estrutura e outros sistemas
de arquivos podem ser associados a diferentes pontos de montagem.

### Vantagens do particionamento

-   separação de dados;
-   isolamento de possíveis falhas;
-   utilização de diferentes sistemas de arquivos;
-   organização do armazenamento;
-   possibilidade de aplicar políticas específicas de segurança e
    montagem.

------------------------------------------------------------------------

# 2. 🗂️ MBR e GPT

## MBR --- Master Boot Record

A estrutura MBR permite organizar o disco utilizando:

-   partições primárias;
-   partição estendida;
-   partições lógicas.

O comando tradicional para gerenciamento de partições MBR é:

``` bash
sudo fdisk /dev/sda
```

Dentro do `fdisk`, a opção `m` apresenta a ajuda disponível.

------------------------------------------------------------------------

## GPT --- GUID Partition Table

A GPT é uma estrutura moderna de particionamento que oferece recursos
adicionais em relação ao MBR.

Entre suas características estão:

-   suporte a grande quantidade de partições;
-   identificação por UUID e outros identificadores;
-   suporte a discos de grande capacidade;
-   integração com sistemas que utilizam UEFI;
-   possibilidade de manter compatibilidade com estruturas MBR em
    determinados cenários.

------------------------------------------------------------------------

## GNU Parted

O `parted` é uma ferramenta de particionamento que pode trabalhar com
diferentes estruturas, incluindo MBR e GPT.

Exemplo:

``` bash
sudo parted /dev/sda
```

Exemplo de criação de uma tabela GPT:

``` text
mklabel gpt
```

Exemplo de criação de uma partição:

``` text
mkpart primary ext4 root 0.0 50GiB
```

------------------------------------------------------------------------

# 3. 🧱 LVM --- Logical Volume Management

O **LVM** cria uma camada de gerenciamento entre os dispositivos físicos
e os volumes utilizados pelo sistema operacional.

### Principais elementos

``` text
Discos/Partições
       ↓
PV — Physical Volume
       ↓
VG — Volume Group
       ↓
LV — Logical Volume
       ↓
Sistema de arquivos
       ↓
Ponto de montagem
```

### Principais vantagens

-   melhor aproveitamento do espaço;
-   volumes identificados por nomes;
-   expansão de volumes;
-   inclusão de novos dispositivos;
-   movimentação de dados;
-   possibilidade de utilizar recursos de espelhamento.

### Conceitos

  Sigla   Nome              Função
  ------- ----------------- ----------------------------------------------
  PV      Physical Volume   Volume físico utilizado pelo LVM
  VG      Volume Group      Grupo que reúne volumes físicos
  LV      Logical Volume    Volume lógico utilizado para armazenar dados

------------------------------------------------------------------------

# 4. 📁 Sistema de arquivos

O sistema de arquivos define como os dados são organizados, armazenados
e recuperados em uma partição.

O Linux possui suporte a diversos sistemas de arquivos.

### Principais exemplos

  Sistema          Característica
  ---------------- -----------------------------------------------------------
  ext2/ext3/ext4   Sistemas de arquivos tradicionais do Linux
  XFS              Sistema de arquivos com journaling
  NTFS             Sistema utilizado principalmente em ambientes Windows
  FAT/vFAT         Compatibilidade com diferentes sistemas
  ISO9660          Utilizado em mídias ópticas
  NFS              Sistema de arquivos utilizado em rede
  SMB              Compartilhamento de arquivos em redes compatíveis com SMB

------------------------------------------------------------------------

# 5. 📝 Journaling

Alguns sistemas de arquivos utilizam **journaling** para registrar
operações antes ou durante sua aplicação no sistema de arquivos.

Esse mecanismo auxilia na recuperação da estrutura do filesystem após
falhas, desligamentos inesperados ou interrupções.

------------------------------------------------------------------------

# 6. 🧩 Blocos e inodes

Durante a criação de um sistema de arquivos são definidos parâmetros
relacionados ao armazenamento.

Entre eles:

-   tamanho dos blocos;
-   quantidade de inodes.

Os **blocos** armazenam os dados.

Os **inodes** armazenam informações sobre os arquivos, como metadados e
referências aos dados.

Para consultar informações detalhadas de sistemas ext:

``` bash
sudo dumpe2fs /dev/sda1
```

------------------------------------------------------------------------

# 7. 🛠️ Criando um sistema de arquivos

O comando `mkfs` prepara uma partição ou dispositivo para utilização com
determinado sistema de arquivos.

Sintaxe geral:

``` bash
mkfs [opções] [-t tipo] dispositivo
```

Exemplo:

``` bash
sudo mkfs -t ext4 /dev/sda1
```

> ⚠️ **Atenção:** formatar uma partição pode apagar os dados existentes.
> Execute o procedimento somente no dispositivo correto.

------------------------------------------------------------------------

# 8. 🏷️ LABEL e UUID

Os dispositivos podem ser identificados por nomes, **LABELs** e
**UUIDs**.

### blkid

Exibe informações dos dispositivos:

``` bash
sudo blkid
```

### e2label

Permite consultar ou alterar o LABEL de sistemas ext:

``` bash
sudo e2label /dev/sdb1
```

Para definir um novo LABEL:

``` bash
sudo e2label /dev/sdb1 dados
```

------------------------------------------------------------------------

# 9. 🔗 Montagem de dispositivos

O Linux utiliza uma árvore única de diretórios. Para disponibilizar uma
partição nessa árvore, é necessário montá-la em um ponto de montagem.

### Criando um ponto de montagem

``` bash
sudo mkdir -p /mnt/dados
```

### Montando

``` bash
sudo mount /dev/sdb1 /mnt/dados
```

### Desmontando

``` bash
sudo umount /mnt/dados
```

------------------------------------------------------------------------

# 10. ⚙️ Arquivo /etc/fstab

O arquivo:

``` text
/etc/fstab
```

contém as definições utilizadas pelo sistema para montar sistemas de
arquivos.

Uma entrada normalmente possui:

``` text
dispositivo  ponto_de_montagem  filesystem  opções  dump  fsck
```

Exemplo:

``` text
/dev/sda5 /home ext4 defaults 1 2
```

Também é possível utilizar UUID:

``` text
UUID=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX /dados ext4 defaults 0 2
```

### Opções comuns

  Opção        Função
  ------------ -------------------------------------------
  `auto`       Permite montagem automática
  `noauto`     Impede montagem automática
  `user`       Permite montagem pelo usuário
  `nouser`     Restringe a montagem ao root
  `users`      Permite montagem/desmontagem por usuários
  `exec`       Permite execução de binários
  `noexec`     Impede execução de binários
  `ro`         Somente leitura
  `rw`         Leitura e escrita
  `sync`       Sincronização imediata
  `async`      Sincronização assíncrona
  `suid`       Habilita SUID/SGID
  `nosuid`     Desabilita SUID/SGID
  `acl`        Habilita suporte a ACL
  `defaults`   Conjunto de opções padrão

------------------------------------------------------------------------

# 11. 📊 Utilização de espaço --- du

O comando `du` apresenta o espaço utilizado por arquivos e diretórios.

Exemplos:

``` bash
du -k /home/aluno
```

``` bash
du -hs /home/aluno/*
```

Para consultar inodes:

``` bash
du --inodes -s /home/aluno
```

------------------------------------------------------------------------

# 12. 💾 Espaço disponível --- df

O comando `df` apresenta informações sobre o espaço utilizado e
disponível nos sistemas de arquivos montados.

Exemplos:

``` bash
df -h
```

Somente determinado filesystem:

``` bash
df -t ext4
```

Espaço e informações de inodes:

``` bash
df -i -T
```

------------------------------------------------------------------------

# 13. 🩺 Verificação do sistema de arquivos

O comando `fsck` é utilizado para verificar a consistência de sistemas
de arquivos e, quando necessário, realizar correções.

Exemplo:

``` bash
sudo fsck /dev/sdb1
```

> ⚠️ Normalmente o filesystem deve estar desmontado antes de uma
> verificação ou reparação. Utilize o procedimento adequado para o
> ambiente.

------------------------------------------------------------------------

# 14. 📦 LVM --- Fluxo básico

Um fluxo típico de criação de armazenamento utilizando LVM é:

``` text
Disco
  ↓
Partição
  ↓
PV
  ↓
VG
  ↓
LV
  ↓
Filesystem
  ↓
Mount Point
```

Comandos principais:

``` bash
pvcreate
pvscan
vgcreate
vgdisplay
lvcreate
lvdisplay
lvextend
```

Exemplo conceitual:

``` bash
sudo pvcreate /dev/sda2
sudo pvcreate /dev/sdb1
```

``` bash
sudo vgcreate vgProducao /dev/sda2 /dev/sdb1
```

``` bash
sudo lvcreate -n lvDadosPublicos -L 5G vgProducao
```

Formatando:

``` bash
sudo mkfs.ext4 /dev/vgProducao/lvDadosPublicos
```

Criando o ponto de montagem:

``` bash
sudo mkdir -p /dados/publico
```

Montando:

``` bash
sudo mount /dev/vgProducao/lvDadosPublicos /dados/publico
```

------------------------------------------------------------------------

# 15. 📈 Redimensionamento de LVM

Uma das vantagens do LVM é permitir alterações no tamanho dos volumes
lógicos.

Exemplo de expansão:

``` bash
sudo lvextend -L +1G /dev/vgProducao/lvDadosPublicos
```

Depois, para um filesystem ext4, pode ser necessário ampliar o sistema
de arquivos:

``` bash
sudo resize2fs /dev/vgProducao/lvDadosPublicos
```

Conferindo:

``` bash
df -h
```

------------------------------------------------------------------------

# 16. 🚦 Sistema de quotas

As quotas permitem controlar a quantidade de espaço que usuários ou
grupos podem utilizar em determinadas partições.

Podem ser utilizadas para:

-   limitar consumo de armazenamento;
-   controlar usuários;
-   controlar grupos;
-   estabelecer limites;
-   acompanhar utilização;
-   evitar que um usuário ocupe todo o espaço disponível.

------------------------------------------------------------------------

# 17. ⚙️ Preparação para quotas

O suporte deve estar disponível no sistema e o pacote de quotas precisa
estar instalado.

A configuração é feita por filesystem.

No `/etc/fstab`, podem ser utilizadas opções como:

``` text
usrquota
```

para controle por usuários.

``` text
grpquota
```

para controle por grupos.

Ou ambas:

``` text
usrquota,grpquota
```

Exemplo:

``` text
/dev/sda5 /home ext4 usrquota,grpquota,defaults 1 2
```

------------------------------------------------------------------------

# 18. 🔄 Inicializando quotas

Após configurar o `/etc/fstab`, pode ser necessário desmontar e montar
novamente a partição ou reiniciar o sistema, dependendo do ponto de
montagem.

Para preparar os arquivos de controle:

``` bash
sudo quotacheck -cug /home
```

O processo pode criar arquivos como:

``` text
aquota.user
aquota.group
```

Para habilitar quotas:

``` bash
sudo quotaon -aug /home
```

Também pode ser utilizado:

``` bash
sudo systemctl enable quotaon.service
```

------------------------------------------------------------------------

# 19. 👤 Gerenciamento de quotas

### edquota

Utilizado para editar quotas de usuários ou grupos.

Exemplo:

``` bash
sudo edquota -u aluno1
```

Para copiar a configuração de quota:

``` bash
sudo edquota -p aluno1 aluno2 aluno3
```

### quota

Consulta a quota de um usuário:

``` bash
quota -u aluno1
```

### repquota

Apresenta informações de quota da partição:

``` bash
sudo repquota -u /home
```

------------------------------------------------------------------------

# 20. 🔍 Atualização das informações de quota

O comando `quotacheck` atualiza as informações utilizadas pelo sistema
de quotas.

Um procedimento comum é:

``` bash
sudo quotaoff -aug /home
```

``` bash
sudo quotacheck -aug /home
```

``` bash
sudo quotaon -aug /home
```

------------------------------------------------------------------------

# 21. 📧 Alertas de quota

O comando `warnquota` pode ser utilizado para gerar avisos aos usuários
que ultrapassarem determinados limites configurados.

``` bash
sudo warnquota
```

------------------------------------------------------------------------

# 22. 🧪 Comandos para laboratório

### Dispositivos

``` bash
lsblk
sudo blkid
```

### Particionamento

``` bash
sudo fdisk -l
sudo fdisk /dev/sdb
sudo parted /dev/sdb
```

### Filesystem

``` bash
sudo mkfs.ext4 /dev/sdb1
sudo fsck /dev/sdb1
```

### Montagem

``` bash
mount
df -h
du -h
sudo mount /dev/sdb1 /mnt
sudo umount /mnt
```

### LVM

``` bash
sudo pvscan
sudo vgdisplay
sudo lvdisplay
```

### Quotas

``` bash
sudo quotacheck -aug /home
sudo quotaon -aug /home
quota -u aluno
sudo repquota -u /home
```

------------------------------------------------------------------------

# 23. 📋 Resumo dos principais comandos

  Comando        Finalidade
  -------------- ------------------------------------------
  `fdisk`        Gerenciamento de partições
  `parted`       Gerenciamento de partições MBR/GPT
  `pvcreate`     Criação de volume físico LVM
  `pvscan`       Consulta de volumes físicos
  `vgcreate`     Criação de grupo de volumes
  `vgdisplay`    Exibição de informações do VG
  `lvcreate`     Criação de volume lógico
  `lvdisplay`    Exibição de informações do LV
  `lvextend`     Expansão de volume lógico
  `mkfs`         Criação de sistema de arquivos
  `blkid`        Consulta de UUID e filesystem
  `mount`        Montagem de filesystem
  `umount`       Desmontagem
  `df`           Espaço disponível/utilizado
  `du`           Espaço utilizado por arquivos/diretórios
  `fsck`         Verificação e reparação
  `quota`        Consulta de quota
  `edquota`      Edição de quota
  `quotacheck`   Atualização das informações de quota
  `quotaon`      Ativação de quotas
  `quotaoff`     Desativação de quotas
  `repquota`     Relatório de quotas
  `warnquota`    Avisos relacionados às quotas

------------------------------------------------------------------------

# 24. 🧠 Mapa mental do capítulo

``` text
                    SISTEMA DE ARQUIVOS
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
 Particionamento          LVM               Quotas
        │                  │                  │
    ┌───┴───┐         ┌────┴────┐        ┌────┴────┐
    │       │         │         │        │         │
   MBR     GPT        PV        VG       Usuário  Grupo
    │                  │         │
  fdisk              VG        LV
  parted                         │
                                 │
                            Filesystem
                                 │
                         ┌───────┴───────┐
                         │               │
                       mount          /etc/fstab
                         │
                    Diretórios
```

------------------------------------------------------------------------

# 25. ✅ Checklist de aprendizagem

-   [ ] Entendi a função do particionamento.
-   [ ] Diferenciei MBR e GPT.
-   [ ] Conheci `fdisk` e `parted`.
-   [ ] Entendi PV, VG e LV.
-   [ ] Conheci o funcionamento básico do LVM.
-   [ ] Entendi a função do sistema de arquivos.
-   [ ] Conheci ext4, XFS, NTFS, NFS, SMB e outros.
-   [ ] Entendi LABEL e UUID.
-   [ ] Aprendi a montar e desmontar dispositivos.
-   [ ] Conheci o `/etc/fstab`.
-   [ ] Aprendi a consultar espaço com `df` e `du`.
-   [ ] Conheci o `fsck`.
-   [ ] Entendi o conceito de quotas.
-   [ ] Aprendi a habilitar e verificar quotas.
-   [ ] Conheci `edquota`, `quota`, `repquota` e `quotacheck`.

------------------------------------------------------------------------

## 👨‍🏫 Professor

**Ygor Silva**

## 📚 Curso

**Administração de Sistemas Linux**

## 📌 Capítulo

**03 --- Sistema de Arquivos**

------------------------------------------------------------------------

⭐ Material organizado para estudo, prática em laboratório e consulta
rápida durante a administração de sistemas Linux.
