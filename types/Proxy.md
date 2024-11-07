# Proxy (Procurador)

O **Proxy** age como um intermediário entre o cliente e o recurso que ele deseja acessar, controlando o acesso a esse recurso. Imagine que você quer falar com o presidente de uma empresa. Em vez de ir direto até ele, você fala com uma secretária que decide se deve ou não passar sua mensagem para o presidente. Essa secretária é o **Proxy**.

### Como funciona o Proxy na programação:

- **Proxy**: O proxy é quem controla o acesso a algo mais "importante" ou "sensível". Ele pode realizar verificações de segurança, fazer cache (armazenar dados para acessar mais rápido) ou até mesmo reduzir o trabalho do recurso principal.
- **Recurso** real: Este é o objeto "real" que o cliente quer acessar. Ele está protegido pelo Proxy e pode ser algo que exige cuidado ao ser usado.

### Exemplo no código: 

Em uma aplicação bancária, um **Proxy** pode controlar o acesso às informações da conta de um cliente. O **Proxy** verifica se o cliente está autenticado e autorizado a ver as informações antes de realmente permitir o acesso.

## Quando usar o Proxy? 

Quando você quer controlar ou monitorar o acesso a um recurso, proteger dados, reduzir o tempo de resposta com cache, ou aplicar regras de segurança.

## Proxy (Procurador) no Vue.js 3

O **Proxy** no frontend pode ser usado para gerenciar a comunicação com APIs, especialmente se há restrições de acesso ou condições que precisam ser verificadas antes de fazer a chamada.

### Exemplo:

Suponha que você tenha uma API que precisa de autenticação. Em vez de expor a API diretamente aos componentes, você pode usar um **Proxy** para gerenciar as chamadas.

#### Implementação no Vue:  
Crie um **Proxy** para gerenciar as chamadas da API:

```javascript
// apiProxy.js
import axios from 'axios';

export const apiProxy = {
  get(url) {
    return axios.get(url, {
      headers: { Authorization: `Bearer ${localStorage.getItem('token')}` },
    });
  },
  post(url, data) {
    return axios.post(url, data, {
      headers: { Authorization: `Bearer ${localStorage.getItem('token')}` },
    });
  },
  // outros métodos de requisição HTTP
};
```

No componente, você usa `apiProxy` em vez de chamar diretamente o axios. Assim, qualquer chamada para a API passa pela verificação de autenticação ou qualquer lógica implementada no **Proxy**.

```javascript
import { apiProxy } from './apiProxy';

async function fetchData() {
  try {
    const data = await apiProxy.get('/endpoint');
    console.log(data);
  } catch (error) {
    console.error('Erro ao buscar dados:', error);
  }
}
```

O **Proxy** cuida de adicionar os headers de autenticação, entre outras regras de acesso que podem existir.
