# Desenvolvimento de apps

> Vamos adotar o termo *apps* em referência a aplicativos desenvolvidos para dispositivos móveis. 
> 
> **Dica de ouro**: pronuncie a palavra *mobile* como *môbol* e não *mobáile*.

O histórico do desenvolvimento de apps acompanha o das suas respectivas plataformas (ou *sistemas operacionais*). No caso do [Android](https://en.wikipedia.org/wiki/Android_version_history), a versão 1.0 foi lançada em 2008 e a mais recente, a 10.0, foi lançada em setembro de 2019. Quanto ao [iOS](https://en.wikipedia.org/wiki/IOS_version_history), a primeira versão foi lançada em 2007 e a mais recente é a 13.2, lançada em outubro de 2019.

A forma mais tradicional de desenvolvimento é conhecida como **nativa**, quando são utilizadas as plataformas de desenvolvimento (SDK), suas linguagens e ferramentas. Enquanto o Android adota o [Java](https://pt.wikipedia.org/wiki/Java) e o [Android Studio](https://developer.android.com/studio), o iOS adota o [Swift](https://www.apple.com/br/swift/) e o [Xcode](https://developer.apple.com/xcode/).

## Desenvolvimento híbrido

Com a popularização de frameworks para desenvolvimento frontend moderno surgiram alternativas para o desenvolvimento de apps que adotaram recursos de desenvolvimento web, como HTML, CSS e JavaScript. Uma das primeiras iniciativas nesse sentido foram o [PhoneGap](https://phonegap.com/) e o [Ionic](https://ionicframework.com/). 

Essa forma de desenvolvimento encontrou no [NodeJS](https://nodejs.org/) uma plataforma chava, permitindo gerenciamento de pacotes e desenvolvimento de software **multiplataforma**: para web, mobile e desktop.

> **Multiplataforma**
> 
> Lembra quando o termo **multiplataforma** (ou *cross-platform*) era restrito ao sistema operacional desktop? Pois é.

O grande objetivo desses frameworks é permitir o **reúso**, ou seja, é possível desenvolver um software em uma única base de código e entregá-lo em múltiplas plataformas.

## Desenvolvimento nativo com tecnologias web

Um grande questionamento a respeito do desenvolvimento híbrido é quanto ao desempenho dos aplicativos, já que eles não necessariamente utilizam os recursos nativos da plataforma (embora possam fazê-lo para algumas tarefas). Para contornar isso temos hoje frameworks de desenvolvimento que permitem ainda trabalhar com tecnologias web, mas entregar software nativo para cada plataforma. Dentre essas encontramos, principalmente:

* [**NativeScript**](https://www.nativescript.org/): um framework de desenvolvimento que suporta Angular, Vue.js e ReactJS
* [**ReactNative**](http://www.reactnative.com/): desenvolvido pelo Facebook, baseado no ReactJS 
* [**Flutter**](https://flutter.dev/): desenvolvido pelo Google, utiliza a linguagem Dart
* [**Kotlin**](https://kotlinlang.org/): desenvolvido pela Jetbrains

## Frameworks de desenvolvimento web moderno

No cenário do desenvolvimento web é comum encontrarmos a utilização de frameworks ou bibliotecas. Utilizando o NodeJS e ferramentas como [Webpack](https://webpack.js.org/) é possível encontrar recursos antes só disponíveis em ferramentas mais tradicionais, como a compilação, checagem de código, testes unitários e empacotamento de *assets*.

Dentre esses frameworks destacam-se atualmente:

* [**Angular**](https://angular.io): desenvolvido pelo Google, é um framework para desenvolvimento moderno e utiliza TypeScript
* [**ReactJS**](https://pt-br.reactjs.org/): desenvolvido pelo Facebook, é uma biblioteca para criar interfaces de usuário
* [**Vue.js**](https://vuejs.org/): é um framework JavaScript para desenvolvimento interfaces gráficas

> **AngularJS vs Angular**
> 
> A primeira versão do Angular, chamada de AngularJS (ou AngularJS 1), é totalmente diferente da versão atual (somente "Angular", sem o "JS"). Há certa confusão ao lidar com esses frameworks, então, quando pesquisar algo no Google, adote **-angularjs** na sua string de busca.

