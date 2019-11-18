# Clonagem de discos

Este repositório faz uma breve revisão de alguns comandos básicos de terminal do linux para depois aprensentar o dd, ferramenta que será usada para clonagem

## Instruções

* Entre no diretório revisão se você não conhece os comandos básicos do linux
* O diretório dd contém instruções de uso do software dd
* O repositório contém alguns exemplos de códigos funcionais que ajudam na resolução da lista. A maioria das questões podem ser resolvidas alterando ou combinando esses códigos. Cada um deles é detalhado na seção a seguir chamada Revisão.
* Para submeter a lista para avaliação basta criar um único arquivo .rar ou .zip contendo todos os códigos implementados. Eles devem ser submetidos via SUAP.
 
## O comando dd

Em geral o dd é usado da seguinte forma:

```shell
dd if = /dev/sda of = /dev/sdb
```



[Tutorial](https://linuxhint.com/completely_wipe_hard_drive_ubuntu/) completo de como fazer data wipe num disco rígido

Uso:
```shell
dd if=/dev/urandom of=/dev/sdX bs=4k
```