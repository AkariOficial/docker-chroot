# Docker-chroot
> Como usar o Docker dentro de um ambiente [chroot-unshare](https://github.com/Moe-hacker/termux-container) no Termux.<br>
> By @AkariOficial
-------------

## Como faz?

### **Instale o tsu** [# o quê é o tsu?](https://github.com/AkariOficial/docker-chroot#tsu)
```bash
 pkg in -y tsu
 tsu
```

### **Habilite o cgroup**:
```bash
 sudo mount -t tmpfs -o uid=0,gid=0,mode=0755 cgroup /sys/fs/cgroup
```

### **Inicie o docker**
```bash
 sudo dockerd --iptables=false &
```

### **Abra outra guia no termux e executa o chroot**:
```bash
 container -run arch
```
> nota: volte para a outra aba, após executar o código acima na etapa 2

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

### Volte para a guia que você executou na etapa [#2.2] <br> e saia do chroot digitando exit e logue novamente.
```bash
 container -run arch
```
**Verificando se tudo ocorreu bem**:
```bash
 docker info
```
> nota: (deve retornar informações da versão do docker e outros parâmetros).

#### Para saber se realmente funcionou,<br> tente executar um container:
```
 docker run hello-world
```
-------------

#### Informações úteis (ou não)

### tsu
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

### docker
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
