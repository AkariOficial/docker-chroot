# Docker-chroot
> Como usar o Docker dentro de um ambiente [chroot-unshare](https://github.com/Moe-hacker/termux-container) no Termux.<br>
> By @AkariOficial
-------------

### Tutorial Vídeo
<details>
<summary>Mostrar mais</summary>

### Como faz?

Telegram: [Assistir Vídeo](https://t.me/upload_akari/6)

</details>

-------------

### Tutorial Texto
<details>
<summary>Mostrar mais</summary>

### Como faz?

### **Instale o tsu** [#o quê é o tsu?](https://github.com/AkariOficial/docker-chroot#tsu)
```bash
 pkg in -y root-repo tsu
 tsu
```

### **Habilite o cgroup** [#o que é cgroup?](https://github.com/AkariOficial/docker-chroot#cgroup-explica%C3%A7%C3%A3o-para-docker)
```bash
 sudo mount -t tmpfs -o uid=0,gid=0,mode=0755 cgroup /sys/fs/cgroup
```

### **Inicie o docker** [#o que é docker?](https://github.com/AkariOficial/docker-chroot#docker)
```bash
 sudo dockerd --iptables=false &
```

### **Abra outra guia no termux e executa o chroot [2.2]**
```bash
 container -run arch
```
> nota: Volte para essa aba [inicie-o-docker](https://github.com/AkariOficial/docker-chroot#inicie-o-docker), após executar **container -run arch** acima.

### **Crie um arquivo chamado** ``docker.sock`` **em** ``chroot/var/run/docker.sock`` **e dê permissão 666**
```bash
 sudo touch arch/var/run/docker.sock; sudo chmod 666 arch/var/run/docker.sock
```
> Partindo do princípio que você sabe o que é um chroot e etc **(este não é um tutorial de chroot em específico).**

### **Expondo o socket do Docker que está localizado fora do ambiente chroot.**
```bash
 sudo mount --bind /data/docker/run/docker.sock /data/data/com.termux/files/home/arch/var/run/docker.sock
```
-------------

### Volte para a guia que você executou na etapa [#2.2](https://github.com/AkariOficial/docker-chroot/blob/main/README.md#abra-outra-guia-no-termux-e-executa-o-chroot-22) <br> e saia do chroot digitando exit e logue novamente.
```bash
 container -run arch
```
**Verificando se tudo ocorreu bem**
```bash
 docker info
```
> nota: (deve retornar informações da versão do docker e outros parâmetros).

#### Para saber se realmente funcionou,<br> tente executar um container:
```
 docker run hello-world
```
> ![Imagem do Docker com Chroot rodando imagem de um hello-world](https://user-images.githubusercontent.com/58480908/227385492-dc42dc9d-b0c2-4931-ac4f-c6bf023b8f0d.png)
-------------

</details>

--------
### Informações úteis (ou não)
> aqui estarão algumas informações do que foi utilizado.

#### tsu
<details>
<summary>Mostrar mais</summary>

```
O comando tsu é uma ferramenta
no Termux que permite obter 
privilégios de superusuário
(root) no terminal. É semelhante
ao comando su que é usado em
sistemas operacionais Linux.
```

</details>

#### docker
<details>
<summary>Mostrar mais</summary>

```
Docker é uma plataforma de 
software que permite criar, 
implantar e executar aplicativos 
em contêineres, que são ambientes 
isolados e leves que executam um 
aplicativo e seus componentes, 
incluindo bibliotecas e dependê-
ncias. 
Isso permite que os aplicativos 
sejam portáteis, escaláveis 
e executados consistentemente 
em diferentes ambientes.
```

</details>

#### cgroup (explicação para docker)
<details>
<summary>Mostrar mais</summary>

> Como já sabemos,  o Docker é uma 
plataforma de software que permite 
criar, implantar e executar aplicativos 
em contêineres. E o que seria o cgroup
em docker? cgroup é uma abreviação para 
"control group", um recurso do kernel do 
Linux que permite limitar, medir e isolar 
os recursos do sistema, como CPU, memória 
e E/S,para processos ou grupos de processos
específicos. <br> O comando ```sudo mount -t tmpfs -o uid=0,gid=0,mode=0755 cgroup /sys/fs/cgroup``` <br> monta o sistema de arquivos "cgroup" em /sys/fs/cgroup usando o tipo "tmpfs" (um sistema de arquivos virtual na memória). Ele especifica o UID (identificador do usuário) e GID (identificador do grupo) como 0, o que significa que apenas o usuário root tem acesso ao sistema de arquivos cgroup. O modo 0755 define as permissões de acesso ao sistema de arquivos, permitindo que os proprietários e outros usuários leiam e executem arquivos, mas apenas o proprietário possa gravar.

</details>

#### chroot-unshare
<details>
<summary>Mostrar mais</summary>

> O chroot-unshare é um recurso do Termux que permite criar um ambiente isolado dentro do sistema operacional Android, como se fosse uma máquina virtual. Esse ambiente pode ser usado para executar programas de outros sistemas operacionais, por exemplo. O comando chroot permite mudar o diretório raiz do sistema para outro diretório, enquanto o comando unshare permite criar um novo espaço de nomes para o processo. Juntos, eles criam um ambiente isolado do resto do sistema operacional.

</details>
