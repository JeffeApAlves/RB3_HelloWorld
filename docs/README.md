# 1. Configuração do ambiente de desenvolvimento

Editar o script .bashrc adicionando na variável de ambiente “PATH” os caminhos de cada toolchain.

```shell
export PATH=$PATH:$HOME/toolchains/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian/bin
export PATH=$PATH:$HOME/toolchains/linaro/gcc-linaro-6.2.1-2016.11-x86_64_arm-linux-gnueabihf/bin
export PATH=$PATH:$HOME/toolchains/x-tools/armv8-rpi3-linux-gnueabihf/bin
```
Deixar ativo apenas um path por vez. Comentando com “#” os demais

# 2.	Testando o ambiente

Os toolchains utilizados nesse ambiente de desenvolvimento, serão executados em uma arquitetura x64, mas criara binários para uma arquitetura target do tipo ARM (core utilizado na raspberry). Portanto teremos um processo de cross-compile.

Utilizando o editor de texto “nano” foi criado o pequeno código de teste em um arquivo <work_space>/main.c

[main.c](https://github.com/JeffeApAlves/app_rb3/blob/master/app)

### 2.1. Toolchain (x-tools)

Através do comando abaixo dentro do diretório onde se encontra arquivo ‘main.c’ criado no passo anterior

```shell
arm-linux-rpi3-gcc <arquivos_codigo_fonte> -o <arquivo_de_saida>`
```
### 2.2 Informações do arquivo de saída (resultado da compilação).

```shell
file <arquivo_de_saida>
strings <arquivo_de_saida>
```

### 2.3 Executando o software na Raspberry

Configurar o flag de execução do arquivo de saída

```shell
sudo chmod +x app
```

Com a raspberry(target) em uma mesma rede onde se encontra o computador host, onde está sendo feito a compilação.

Enviar o arquivo utilizando o comando

```shell
rsync -avz <arquivo_de saida> <usuario_rb3>@<ip_da_rb3>:<deploy_path>
```

Abrir uma sessão ssh

```shell
ssh <usuario_rb3>@<ip_da_rb3>
```

Rodar a aplicação 

```shell
<deploy_path>/app
```
