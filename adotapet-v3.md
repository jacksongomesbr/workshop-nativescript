# Versão 3

> Se quiser acompanhar o código completo desta versão acesse https://play.nativescript.org/?template=play-ng&id=4zfO6B&v=3

Já sabemos como usar algumas das opções de layout do NativeScript, bem como componentes para apresentar texto, imagem e botões. 

Na versão atual vamos trabalhar com o seguinte requisito:

* como usuário eu quero ver uma lista com animais disponíveis para adoção. A lista deve apresentar: foto, nome, cidade, estado, espécie, sexo e porte (P, M, G).
* como usuário eu quero ver os detalhes de um animal disponível para adoção. Devem ser apresentadas as informações: : foto, nome, cidade, estado, espécie, sexo e porte (P, M, G).

Para implementar esse requisito vamos começar adicionando o array `animais` no controller do `HomeComponent`:

```typescript
animais = [
    {
        id: 1,
        nome: 'Star',
        foto: 'https://site.com/foto.jpg',
        cidade: 'São Paulo',
        estado: 'SP',
        especie: 'cachorro',
        sexo: 'F',
        porte: 'M'
    },
]
```

Continuando a lógica de esconder/mostrar componentes para simular a navegação de telas, vamos definir mais duas telas: uma para mostrar a lista dos animais e outra para mostrar os detalhes de um animal.

## Lista dos animais

Para apresentar a lista vamos utilizar o componente `ListView`. Adicione o seguinte ao template:

```html
<StackLayout *ngIf="tela == 'passo4'" class="lista">
    <Label textWrap="true"
        text="Encontre um peludo para chamar de seu" class="h2">
    </Label>
    <ListView class="list-group" [items]="animais"
        (itemTap)="onItemTap($event)" style="height:1250px">
        <ng-template let-animal="item">
            <GridLayout columns="60, *" class="list-group-item"
                [data-id]="animal.id">
                <Image [src]="animal.foto" class="thumb img-circle"
                    col="0" verticalAlignment="center">
                </Image>
                <GridLayout rows="auto, auto, auto" col="1">
                    <Label [text]="animal.nome" class="animal-nome"
                        row="0"></Label>
                    <StackLayout orientation="horizontal" row="1">
                        <Label [text]="animal.cidade"></Label>
                        <Label text=" / "></Label>
                        <Label [text]="animal.estado"></Label>
                    </StackLayout>
                    <GridLayout columns="auto, *" row="2">
                        <StackLayout orientation="horizontal" col="0">
                            <Label text="P" class="animal-porte"
                                [class.porte-ativo]="animal.porte == 'P'">
                            </Label>
                            <Label text="M" class="animal-porte"
                                [class.porte-ativo]="animal.porte == 'M'">
                            </Label>
                            <Label text="G" class="animal-porte"
                                [class.porte-ativo]="animal.porte == 'G'">
                            </Label>
                        </StackLayout>
                        <Label horizontalAlignment="right"
                            class="animal-sexo" col="1"
                            [text]="animal.sexo"
                            [class.sexo-f]="animal.sexo == 'F'"
                            [class.sexo-m]="animal.sexo == 'M'">
                        </Label>
                    </GridLayout>
                </GridLayout>
            </GridLayout>
        </ng-template>
    </ListView>
</StackLayout>
```

Vamos por partes. Primeiro, estamos usando um `StackLayout` contendo `Label` e `ListView` para apresentar, respectivamente, o título da tela e a lista dos animais. 

No `ListView` temos `(itemTap)="onItemTap($event)"`, o que indica que o método `onItemTap()` será chamado quando o evento `itemTap` for disparado. Esse evento é disparado quando um item do `ListView` é pressionado. No controller temos a implementação desse método:

```typescript
onItemTap(args): void {
    this.tela = 'passo5';
    this.animal = this.animais[args.index];
}
```

O parâmetro `args` possui o atributo `index`, que indica o índice do item da lista que foi pressionado. Usamos isso para obter o elemento desse índice no array `animais` e o atribuímos a `animal` (que será usado para a tela de mais informações do animal). Além disso, mudamos o valor da variável `tela` para `passo5` (que corresponde à tela de mais informações).

No `ListView` também temos `[items]="animais"`, o que representa a utilização do recurso de **data binding**: o atributo `items` está vinculado ao atributo `animais` (o array que comentamos anteriormente). A sintaxe para fazer usso desse recurso é colocar o nome do atributo entre colchetes. Fazer com que os itens do `ListView` fiquem vinculados ao array significa que temos tantos elementos (itens) no `ListView` quanto os elementos no array.

Para definir a interface dos itens do `ListView` usamos o elemento `ng-template`. Esse elemento não é visível, mas contém elementos visíveis. O atributo `let-animal="item"` é importante porque ele determina que existe uma variável interna ao template chamada "animal" e ela recebe cada item do `ListView`.

A partir daí começamos a fazer uso intenso dos contêineres de layout. Primeiro, usamos um `GridLayout` cujo atributo `columns` tem valor `60, *`, o que significa que ele terá duas colunas: a primeira com largura 60 e a outra com largura correspondente ao espaço restante na tela. Esse elemento também tem `class="list-group-item"`, que é uma classe padrão do NativeScript para estilo de itens de listas. 

O conteúdo do `GridLayout` começa com um `Image`, que mostra a foto do animal. Para fazer isso usamos novamente data binding em `[src]="animal.foto"` para que a URL da imagem seja o atributo `foto` do animal. Ainda aplicamos duas classes padrão do NativeScript: `thumb` e `img-circle`. Para concluir, como essa é a imagem que fica na primeira coluna, temos o atributo `col` com valor `0`.

Na sequência temos outro `GridLayout`, que é usado para mostrar mais informações do animal. Nesse caso temos três linhas com alturas ajustadas e correspondentes aos seus conteúdos -- fazemos isso usando `rows="auto, auto, auto"`. A partir de então passamos a definir o conteúdo dessas três linhas:

* usando `Label` para mostrar o nome do animal
* usando `StackLayout` com orientação horizontal (atributo `orientation`) para mostrar a cidade e o estado
* usando `GridLayout` para mostrar o porte e o sexo (usando novamente componentes já conhecidos).

Ao mostrar o porte usamos data binding com um propósito diferente: ao invés de mostrar o valor temos o objetivo de aplicar uma classe do CSS se uma condição for satisfeita. Isso é usado em:

```html
<Label text="P" class="animal-porte" 
    [class.porte-ativo]="animal.porte == 'P'">
</Label>
```

A sintaxe `[class.porte-ativo]` aplica a classe `porte-ativo` se o atributo `porte` do animal tiver valor `'P'`.

As classes CSS que usamos são:

```css
.home-panel Label {
    margin-bottom: 30;
}

.h2 {
    padding: 20;
}

Image {
    margin-right: 30;
}

.animal-nome {
    font-size: 20;
    font-weight: bold;
}
.animal-porte {
    padding: 5;
    border-color: lightgray;
    border-width: 1;
    border-radius: 5;
    color: lightgray;
    margin-right: 5;
}
.porte-ativo {
    border-color: darkgray;
    border-width: 1;
    color: black;
    font-weight: bold;
}
.animal-sexo {
    padding: 5;
    border-radius: 5;
    color: white;
    font-weight: bold;
}
.sexo-f {
    background-color: pink;
}
.sexo-m {
    background-color: lightblue;
}
```

## Apresentando informações detalhadas do animal

Para a tela com as informações detalhadas do animal usamos as mesmas técnicas anteriores:

```html
<StackLayout *ngIf="tela == 'passo5'" class="detalhes">
    <Label textWrap="true" [text]="animal.nome" class="h2"></Label>
    <Image [src]="animal.foto" verticalAlignment="center"
        stretch="aspectFill" marginRight="0"></Image>
    <Label textWrap="true"
        [text]="animal.cidade + '/' + animal.estado" padding="20">
    </Label>
    <GridLayout columns="auto, *" padding="20">
        <StackLayout orientation="horizontal" col="0">
            <Label text="P" class="animal-porte"
                [class.porte-ativo]="animal.porte == 'P'">
            </Label>
            <Label text="M" class="animal-porte"
                [class.porte-ativo]="animal.porte == 'M'">
            </Label>
            <Label text="G" class="animal-porte"
                [class.porte-ativo]="animal.porte == 'G'">
            </Label>
        </StackLayout>
        <Label horizontalAlignment="right" class="animal-sexo" col="1"
            [text]="animal.sexo" [class.sexo-f]="animal.sexo == 'F'"
            [class.sexo-m]="animal.sexo == 'M'">
        </Label>
    </GridLayout>
</StackLayout>
```

Usamos o `StackLayout` contendo:

* `Label`, para apresentar o nome do animal (veja o uso do data binding)
* `Image`, para apresentar a foto (veja o uso dos atributos `stretch` e `marginRight`)
* `Label`, para apresentar a cidade e o estado (veja outro uso de data binding)
* `GridLayout` para mostrar o porte e o sexo do animal (da mesma forma como fizemos na lista)

O resultado até agora é algo mais ou menos assim.

![](img/adotapet-v3/home.gif)

Agora que estamos fazendo uso mais constante dos contêineres de layout é importante ter mais acesso aos detalhes da documentação: https://docs.nativescript.org/angular/ui/layouts/layout-containers.
