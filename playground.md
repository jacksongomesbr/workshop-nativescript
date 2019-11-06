# Desce pro play!

O [**Playground**](https://play.nativescript.org/) é um recurso do NativeScript que é muito útil no início do desenvolvimento com essa plataforma porque permite iniciar o desenvolvimento sem necessidade de configurações e instalações, ou seja, sem requerer um ambiente de desenvolvimento local. O Playground é um software web e funciona diretamente no browser.

A figura a seguir dá uma visão geral da arquitetura do Playground.

![Visão geral da arquitetura do Playground](https://i.imgur.com/BjCBNYF.png)

Os elementos da arquitetura mostram que o **webserver** entrega o software e utiliza recursos da nuvem da Amazon (S3, DynamoDB, S3, CloudFront) e envia os arquivos do projeto para o **Preview App** usando uma tecnologia chamada [**PubNub**](https://www.pubnub.com/).

## Playgound App

É um leitor de QR code. O Playground gera um QR code que é utilizado para abrir o aplicativo no **Preview App**.

## Preview App

É um *container app*, usado para executar o código do software desenvolvido no Playground diretamente no dispositivo físico (smartphone).

## A mágica!

![](https://d2odgkulk9w7if.cloudfront.net/images/default-source/blogs/playground40eb662a7b776b26a649ff04000922f2.gif?sfvrsn=be9c0dfe_0)

1. quando você cria uma sessão no Playground você seleciona o template e os arquivos são carregados no editor
2. quando você pressiona *Preview* pela primeira vez um QR code é apresentado. Ele contém um código único que gerado para comunicação entre o browser e o aplicativo
3. quando você lê o código com o *Playground App* a informação lida é passada para o *Preview App*
4. quando o *Preview App* inicia ele lê o código da comunicação e o utiliza para criar um canal de comunicação diretamente com o browser
5. o browser recebe uma mensagem do dispositivo conectado e envia dos arquivos pelo canal de comunicação
6. o *Preview App* lê os arquivos e os armazena em uma pasta no sistema de arquivos do dispositivo
7. se algum arquivo foi alterado no browser, o *Preview App* reinicia (somente arquivos alterados são enviados para o dispositivo)

