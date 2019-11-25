# Roteiro de aula prática

Equipamentos necessários a prática:

* Computador funcional

* Pendrive ou cdrom com live-cd do Ubuntu 18.04 ou equivalente

## Objetivo

O objetivo dessa prática é recuperar arquivos de uma partição que foi formatada.

1. Crie uma nova partição no seu disco rígid
1. Formate a partição recém criada 
1. Coloque algumas imagens, pdfs e quaisquer outros tipos de arquivo nessa partição.

Nas seções a seguir detalha-se cada ponto para realização da recuperação dos dados.

## Criando a partição

Use o programa `gparted` para criar uma nova partição no seu disco rígido. Para a aula recomenda-se que a partição seja bem pequena para diminuir o tempo de processamento da clonagem e recuperação. Recomenda-se, por exemplo, o uso de uma partição de 100 MB.

Para iniciar o gparted como administrador basta usar o comando no terminal:

```shell
sudo gparted
```

## Formatando a partição recém criada

Use o `gparted` para formatar a partição recém criada para o sistema de arquivo `fat 32`, por exemplo.

### Coloque arquivos na partição



Aqui temos um breve resumo sobre clonagem de discos e partições usando o software dd. Existe um repositório mais completo sobre clonagem que pode ser encontrado [aqui](https://github.com/jp-guimaraes/clonagem). Lá pode ser encontrado uma revisão de alguns comandos básicos de terminal do linux para depois aprensentar o `dd`, ferramenta usada para clonagem.

### O comando dd

Em geral o `dd` é usado da seguinte forma:

```shell
dd if=/dev/sda1 of=/dev/sdb2
```
`if=/dev/sda1` é a primeira partição do disco a que será clonada para a segunda partição do disco b, `/dev/sdb2`


### Como fazer data wipe num disco rígido

Uso:

```shell
dd if=/dev/urandom of=/dev/sdX bs=4k
```

### O programa `foremost`

O [foremost](https://github.com/korczis/foremost) é um software livre que busca por cabeçalhos de arquivos com o objetivo de recuperar arquivos em partições e discos. Por essa característica de buscar cabeçalhos, pode-se usar esse software para recuperar inclusive arquivos deletados ou de partições/discos formatados.

Para usar o foremost para recuperar arquivos basta passar os tipos de arquivos que se deseja buscar pelos cabeçalhos, o arquivo ou partição de entrada e um diretório de saída onde os arquivos recuperados serão armazenados. Usa-se `-t all` para buscar por todas as extensões de arquivos possíveis.

```shell
foremost -t all -i arquivo_de_entrada -o diretorio_de_saida
```

### Roteiro de recuperação

1. Clonar partição alvo e gerar aquivo iso equivalente

```shell
dd if=/dev/particao_alvo of=/localizacao_do_arquivo
```

1. Criar diretório para receber arquivos recuperados
```shell
mkdir dir_arquivos_recuperados
```
1. Rodar foremost buscando por todos os cabeçalhos de arquivos possíveis na imagem criada

```shell
foremost -t all -i localizacao_do_arquivo -o dir_arquivos_recuperados
```

Ao final do processamento, um arquivo .txt é gerado com o resumo do procedimento.