# Builder (Construtor)

O **Builder** é um padrão que foca em construir objetos complexos em várias etapas. Vamos pensar em um restaurante onde você monta seu sanduíche. Você começa escolhendo o pão, depois escolhe os recheios, molhos e outros complementos. Cada pessoa pode montar seu sanduíche de forma diferente, mas o processo segue sempre o mesmo passo a passo. Aqui, o sanduíche final é o `produto`, e o funcionário que monta o sanduíche é o `construtor`.

### Como funciona o Builder na programação:

- **Diretor**: Ele é o responsável por controlar o processo de construção. No caso do restaurante, o diretor seria o menu, que diz ao funcionário em qual ordem as partes do sanduíche devem ser adicionadas.
- **Construtor**: O construtor é quem realmente cria o objeto, passo a passo, montando cada parte de acordo com o pedido.

### Exemplo no código: 

Imagine que você está criando uma aplicação onde os usuários podem personalizar um carro. Eles escolhem o modelo, a cor, as rodas e o motor. Cada um desses é um "passo" no processo de construção, e o Builder organiza tudo isso, garantindo que o carro seja montado corretamente.

## Quando usar o Builder? 

Quando você precisa criar objetos complexos que têm muitas partes ou configurações diferentes, e quer que isso seja feito passo a passo de forma organizada.

## Builder (Construtor) no Vue.js 3

O padrão Builder é útil para criar objetos complexos, o que no frontend pode incluir um formulário configurável ou um componente que tem várias variações. Podemos usar o Builder para construir configurações para um componente complexo.

### Exemplo:
Imagine que você tem um componente Card que pode ter diferentes layouts, cores e tamanhos. O Builder pode ajudar a construir esses objetos complexos de maneira flexível e reutilizável.

### Implementação no Vue:  
Crie uma função Builder para configurar o card:

```javascript
// cardBuilder.js
export function cardBuilder() {
  let title = '';
  let content = '';
  let color = 'blue';
  let size = 'medium';

  return {
    setTitle(newTitle) {
      title = newTitle;
      return this;
    },
    setContent(newContent) {
      content = newContent;
      return this;
    },
    setColor(newColor) {
      color = newColor;
      return this;
    },
    setSize(newSize) {
      size = newSize;
      return this;
    },
    build() {
      return { title, content, color, size };
    },
  };
}
```

Então, em um componente Vue, você pode usar o Builder para criar configurações do Card:

```javascript
import { cardBuilder } from './cardBuilder';

const myCard = cardBuilder()
  .setTitle('Título do Card')
  .setContent('Conteúdo do Card')
  .setColor('green')
  .setSize('large')
  .build();
```

Essa configuração do card pode ser passada para um componente `Card` que renderiza conforme a configuração do builder. Isso torna o processo de criar e configurar o `Card` mais modular e organizado.