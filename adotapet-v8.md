# Versão 8

> Você pode acompanhar o código completo dessa versão acessando https://play.nativescript.org/?template=play-ng&id=4zfO6B&v=10

Nesta versão vamos implementar os requisitos:

* o software não deve apresentar a barra de ação na tela inicial, apenas nas telas de lista e detalhes
* o software deve apresentar uma imagem de fundo na tela inicial
* o software deve apresentar um indicador de carregamento dos dados nas telas lista e detalhes

## Ocultando a barra de ação no `HomeComponent`

Para implementar esses requisitos vamos começar pela tela `HomeComponent`. Primeiro, removendo o elemento `ActionBar` do template e, no controller, adicionando a importação:

```typescript
import { Page } from "tns-core-modules/ui/page";
```

Depois, injetando o serviço `Page` e modificando o método `ngOnInit()`:

```typescript
constructor(private router: Router, private page: Page) {
}

ngOnInit(): void {
    this.page.actionBarHidden = true;
}
```

Isso faz com que o serviço `Page` esteja disponível no componente. No método `ngOnInit()` esse serviço é usado para ocultar a barra de ação (que aparece por padrão, mesmo que ela não esteja declarada explicitamente no template).

## Mostrar uma imagem de fundo na tela inicial

O arquivo `app/assets/adotapet-home-bg.jpg` será usada na tela inicial. Para isso, adicione a regra a seguir no arquivo CSS do `HomeComponent`:

```css
#main {
  background-size: cover;
  background-image: url("~/assets/adotapet-home-bg.jpg");
}
```

A regra aplicada ao elemento com id `main` define o background do elemento. Para concluir, no template, adicione `id="main"` no primeiro `GridLayout`.

## Mostrando a barra de ação nos componentes lista e detalhes

Para mostrar a barra de ação nas telas `ListaComponent` e `DetalhesComponent` basta adicionar o elemento `ActionBar` no início do template de cada um:

```html
<ActionBar title="AdotaPet"></ActionBar>
```

## Mostrando um indicador de carregamento dos dados

Vamos começar pelo template do `ListaComponent`:

```html
<ActionBar title="AdotaPet"></ActionBar>

<StackLayout class="lista">
...
    <ListView class="list-group" [items]="animais" style="height:1250px"
        [class.visible]="!isBusy">
...
    </ListView>

    <ActivityIndicator [busy]="isBusy" 
        [visibility]="isBusy ? 'visible' : 'collapse'"
        horizontalAlignment="center" verticalAlignment="center">
    </ActivityIndicator>
</StackLayout>
```

O componente `ActivityIndicator` é usado para mostrar um ícone que indica que está ocorrendo um processamento ou carregamento de dados. No controller, adicione o atributo `isBusy`:

```typescript
isBusy: boolean = true;
```

Além disso, modificamos o método `ngOnInit()` para usar o método `subscribe()`:

```typescript
ngOnInit(): void {
    this.db.lista().subscribe(dados => {
        this.isBusy = false;
        this.animais = dados;
    });
}
```

Com isso o atributo `isBusy` tem o valor `true` quando os dados estão carregando (tornando visível o `ActivityIndicator`) e `false` quando os dados já tiverem sido carregados (ocultando o `ActivityIndicator` e mostrando o `ListView`).

Adotamos a mesma técnica no `DetalhesComponent`. O resultado é mais ou menos como o seguinte.

![](img/adotapet-v8/app.gif)
