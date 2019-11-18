# Recuperacao de dados
Aula sobre recuperação de dados

# Edite o texto a para organizar pesquise por  Markdown (Linguagem de marcação de texto )


## Introdução

**Qual é o componente mais valioso de um computador?**

Você pode sugerir, num primeiro momento, que seria o processador. Em geral, o processador é o componente mais caro de um computador. A não ser que você queira investir numa placa de vídeo de ponta, ou numa placa-mãe cheia de novidades. Todas essas alternativas estão considerando valor econômico das partes do computador, mas será mesmo que valioso é aquilo que tem um preço alto?

Há quem diga que o que é realmente valioso é aquilo que é difícil de ser substituído. Por isso preços mais altos são naturalmente relacionados a itens mais valiosos. Então eu pergunto, quanto custa os seus dados?
Faltando um dia para a entrega do seu trabalho de fim de curso, por acidente, você deleta o arquivo. Você perdeu tudo. E agora? Quanto você pagaria para tê-lo novamente? Os dados do usuário são a coisa mais importante num computador. Todo o resto é substituível, mas tem um preço. E é impossível precificar aquela foto especial que estava armazenada no disco rígido do computador que foi roubado, por exemplo.

Por isso, nessa aula pretende-se mostrar várias estratégias de manutenção corretiva e preventiva relacionadas ao armazenamento de dados.

Os slides usados na aula podem ser encontrados [aqui](https://jp-guimaraes.github.io/data_recovery). Eles vão sendo atualizados aos poucos. Se quiser contribuir para essa aula, o código pode ser encontrado [aqui](https://github.com/jp-guimaraes/data_recovery). Comentários, críticas e dúvidas também são sempre bem-vindas, basta enviar um e-mail para <joao.guimaraes@ifrn.edu.br>. 

## Técnicas de recuperação de dados

* Manutenção Corretiva
* Manutenção Preventiva

Recuperar, mas por quê?
* Dados inacessíveis
*	Sistema Operacional?
*	Foram deletados?
*	Lixeira
* Nuvem
	
## Estratégias de Backup
* Importância 
* Tipos de backup
* RAID
* Sistema Operacional
  * Linux
    Script
  * Windows
    Tasker
* Nuvem

## RAID

## Recuperação de dados em partições e discos formatados
Para recuperar dados em partições e discos formatados/deletados é recomendado o procedimento de clonagem.

## Clonagem de discos
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

### Roteiro de recuperação usando `foremost`

Para usar o foremost para recuperar arquivos basta passar os tipos de arquivos que se deseja buscar pelos cabeçalhos, o arquivo ou partição de entrada e um diretório de saída onde os arquivos recuperados serão armazenados. Usa-se `-t all` para buscar por todas as extensões de arquivos possíveis.
```shell
foremost -t all -i arquivo_de_entrada -o diretorio_de_saida
```


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