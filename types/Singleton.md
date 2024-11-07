# Singleton (Único)

O **Singleton** é um padrão que garante que apenas uma única instância de um objeto exista no sistema, e todos que precisarem dele vão compartilhar essa mesma instância. Imagine que em uma escola, todos os professores compartilham um único quadro branco móvel. Se alguém já está usando, ninguém pode criar outro igual – todos esperam até que o quadro esteja disponível.

### Como funciona o Singleton na programação:

- **Instância única**: O Singleton cria apenas uma instância do objeto. Sempre que outra parte do sistema precisa desse objeto, ela vai receber a mesma instância, nunca uma nova.
- **Controle de acesso**: O Singleton controla quem pode criar ou acessar essa instância.

### Exemplo no código:

Em um aplicativo de controle remoto de TV, você quer que só exista uma única instância do controle, para que todos os comandos venham do mesmo lugar e não haja duplicidade de ações.

## Quando usar o Singleton? 

Quando você precisa de um objeto único no sistema, como um controlador de impressão que organiza as impressões em fila, ou uma conexão de banco de dados que todos os usuários compartilham.

## Singleton (Único) no Vue.js 3

O **Singleton** é útil no frontend para garantir que certos serviços ou estados sejam únicos e consistentes em toda a aplicação. Por exemplo, um serviço de gerenciamento de sessão ou uma instância de configuração.

### Exemplo:
Suponha que você tenha um serviço que controle as configurações globais da aplicação. Usando **Singleton**, garantimos que só exista uma única instância dessas configurações.

#### Implementação no Vue:  
Crie um serviço **Singleton** para configurações globais.

```javascript
// settings.js
let instance;

class Settings {
  constructor() {
    if (instance) {
      return instance;
    }
    this.theme = 'light';
    this.language = 'pt-BR';
    instance = this;
  }

  setTheme(newTheme) {
    this.theme = newTheme;
  }

  setLanguage(newLanguage) {
    this.language = newLanguage;
  }
}

export const settingsInstance = new Settings();
```

No componente Vue, você usa o `settingsInstance` para acessar ou modificar as configurações globais, garantindo que todos os componentes vejam sempre a mesma instância.

```javascript
import { settingsInstance } from './settings';

settingsInstance.setTheme('dark'); // Modifica o tema para escuro em toda a aplicação

```

Agora, `settingsInstance` é um objeto **Singleton**. Qualquer alteração nele afeta todos os componentes que o utilizam, garantindo consistência nas configurações globais.