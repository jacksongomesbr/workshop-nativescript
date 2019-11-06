# NativeScript

**NativeScript** é um framework para desenvolvimento de multiplataforma que permite o desenvolvimento de software para iOS e Android, usando Angular, TypeScript ou JavaScript.

As formas de desenvolver software com NativeScript são:

* **NativeScript Playground**: é um ambiente de desenvolvimento direto no browser e é indicado para o início do desenvolvimento
* **NativeScript CLI**: utiliza NodeJS e o SDK de cada plataforma nativa para utilizar recursos mais avançados, extendendo as possibilidades do Playground ao ir na direção de um ambiente de desenvolvimento local
* **Sidekick**: uma ferramenta que pode ser utilizada no ambiente local de desenvolvimento e fornece recursos como templates, plugins e cloud builds

> **cloud builds**
> 
> O recurso *cloud build* fornece a habilidade de compilar o código na nuvem, ao invés de usar o ambiente de desenvolvimento local. O que se ganha com isso é a possibilidade de compilar para iOS sem estar usando o macOS, por exemplo.

## Como NativeScript funciona?

A arquitetura do NativeScript contém diversas partes e é ilustrada pela figura a seguir.

![Arquitetura do NativeScript](https://docs.nativescript.org/img/ns-common.png)

A figura mostra que, na base, a arquitetura requer os componentes nativos de cada plataforma (Android, iOS) e também fornece plugins nativos.

Na sequência, de baixo para cima, o **runtime** fornece uma API que intermedia chamadas nativas a cada plataforma. 

Depois, temos os módulos principais e plugins.

Por fim, antes do código da aplicação, temos o framework e aqui diferenciamos a forma de desenvolvimento conforme a adoção de JavaScript, Angular, Vue e React.

O NativeScript CLI constrói o software para cada plataforma.
