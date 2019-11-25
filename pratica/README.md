# Roteiro de aula prática

Equipamentos necessários a prática:

* Computador funcional

* Pendrive ou cdrom com live-cd do Ubuntu 18.04 ou equivalente

## Objetivo

O objetivo dessa prática é recuperar arquivos de uma partição que foi formatada.

1. Crie uma nova partição no seu disco rígid
1. Formate a partição recém criada (partição alvo)
1. Inclua arquivos na partição alvo
1. Formate a partição alvo
1. Clone a partição alvo
1. Realize o procedimento de data wipe na partição alvo
1. Crie um segundo arquivo clone da partição alvo
1. Tente recuperar os dados usando o `foremost` nos dois arquivos contendo as cópias das partições alvo

Nas seções a seguir detalha-se cada ponto dessa aula prática.

## Criando a partição

Use o programa `gparted` para criar uma nova partição no seu disco rígido. Para a aula recomenda-se que a partição seja bem pequena para diminuir o tempo de processamento da clonagem e recuperação. Recomenda-se, por exemplo, o uso de uma partição de 100 MB.

Lembre-se que para iniciar o gparted como administrador basta usar o comando no terminal:

```shell
sudo gparted
```

## Formatando a partição recém criada

Use o `gparted` para formatar a partição recém criada para o sistema de arquivo `fat 32`, por exemplo.

### Coloque arquivos na partição

Coloque algumas imagens, pdfs e quaisquer outros tipos de arquivo nessa partição.
Um .zip exemplo pode ser encontrado [aqui](https://raw.githubusercontent.com/jp-guimaraes/data_recovery/master/assets/arquivos_exemplo.zip).

Para montar a partição use o comando `mount`

```shell
sudo mount -t auto /dev/sdXY /tmp/
```

onde X é a letra do disco que contém a partição alvo e Y e o número da partição alvo. Exemplo: sda3.

E depois faça a cópia dos arquivos dentro do diretório teste dentro do arquivo .zip para o `/tmp`

```shell
sudo cp -r * . /tmp
```

### Formate a partição alvo

Certifique-se que a partição alvo foi desmontada:

```shell
sudo umount /tmp
```

Essa formatação pode ser feita direto pelo `gparted`. Clique com o botão direito na partição alvo e formate-a para o sistema de arquivo `fat 32`, por exemplo.

### Clone a partição alvo

Recomenda-se a ferramenta `dd`. Para mais detalhes consulte [aqui](https://github.com/jp-guimaraes/clonagem)

```shell
dd if=/dev/sda3 of=/home/usuario/clone1.iso
```

### Realize o procedimento de data wipe na partição alvo

O próprio `dd` pode ser usado para fazer o procedimento de data wipe na partição alvo.
Veja:

```shell
dd if=/dev/urandom of=/dev/sd3 bs=4k
```

### Crie um segundo arquivo clone da partição alvo

```shell
dd if=/dev/sda3 of=/home/usuario/clone2.iso
```

### Tente recuperar os dados usando o `foremost` nos dois arquivos contendo as cópias das partições alvo

Use o [foremost](https://github.com/korczis/foremost) para buscar por cabeçalhos de arquivos nas imagens da partição alvo.

Se o seu computador estiver conectado a internet basta fazer

```shell
sudo apt-get install foremost
```

Caso contrário, você pode baixar [aqui](https://raw.githubusercontent.com/jp-guimaraes/data_recovery/master/assets/foremost_1.5.7-6_i386.deb) a versão 32bits ou [aqui](https://raw.githubusercontent.com/jp-guimaraes/data_recovery/master/assets/foremost_1.5.7-6_amd64.deb) a versão 64 bits desse programa.
Para instalar o `.deb` basta executar:

```shell
sudo dpkg -i nome_do_pacote
```

Não esqueça de criar os dois diretórios de saida diferentes usando o `mkdir`

```shell
mkdir nome_do_diretorio
```

```shell
sudo foremost -t all -i /home/usuario/clone1.iso -o diretorio_de_saida1
```

e depois,

```shell
sudo foremost -t all -i /home/usuario/clone2.iso -o diretorio_de_saida2
```

Compare o resultado dos dois diretórios num relatório endereçado a joao.guimaraes@ifrn.edu.br
