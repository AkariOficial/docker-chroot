# Docker-chroot
> Como usar o Docker dentro de um ambiente [chroot-unshare](https://github.com/Moe-hacker/termux-container) no Termux.<br>
> By @AkariOficial
-------------

### Tutorial Vídeo
<details>
<summary>Mostrar mais</summary>

## Como faz?

```
 video aqui daqui a pouco...
```

</details>

-------------

### Tutorial Texto
<details>
<summary>Mostrar mais</summary>

## Como faz?

### **Instale o tsu** [# o quê é o tsu?](https://github.com/AkariOficial/docker-chroot#tsu)
```bash
 pkg in -y tsu
 tsu
```

### **Habilite o cgroup**
```bash
 sudo mount -t tmpfs -o uid=0,gid=0,mode=0755 cgroup /sys/fs/cgroup
```

### **Inicie o docker**
```bash
 sudo dockerd --iptables=false &
```

### **Abra outra guia no termux e executa o chroot [2.2]**
```bash
 container -run arch
```
> nota: Volte para essa aba [inicie-o-docker](https://github.com/AkariOficial/docker-chroot/blob/main/README.md#inicie-o-docker), após executar **container -run arch** acima.

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
