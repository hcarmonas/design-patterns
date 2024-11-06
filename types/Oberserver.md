# Observer (Observador)

O Observer é um padrão que segue o princípio de "notificar". Imagine uma professora em uma sala cheia de alunos. Se ela mudar algo no quadro, ela vai avisar todos para que prestem atenção. Aqui, a professora é o "sujeito" (ou "observável"), e os alunos são os "observadores". Sempre que o quadro muda, todos os alunos (observadores) são notificados dessa mudança.

## Como funciona o Observer na programação:

- **Sujeito (Observável)**: Esse é o objeto que detém a informação ou estado que pode mudar.
- **Observadores**: Esses são os objetos que ficam "de olho" no sujeito. Quando algo muda no sujeito, ele avisa os observadores.

### Exemplo no código:

Imagine uma aplicação de rede social. Se alguém posta uma nova foto, todos os seguidores dessa pessoa recebem uma notificação. Cada seguidor é um observador, e a pessoa que postou é o sujeito.

## Quando usar o Observer?

Quando você tem uma situação onde várias partes do seu sistema precisam ser avisadas de uma mudança que ocorre em um objeto específico.

## Observer (Observador) no Vue.js 3

No Vue, o padrão Observer é bastante útil para lidar com notificações e mudanças de estado entre componentes. Podemos usar o sistema de eventos do Vue ou um store (como o Vuex ou o Pinia) para implementar o Observer.

### Exemplo:
Imagine uma aplicação de chat onde você tem vários componentes que precisam ser atualizados quando chega uma nova mensagem.

Sujeito (observável): O backend de mensagens ou um store onde as mensagens são armazenadas.  
Observadores: Componentes de chat na interface que exibem as mensagens.  

#### Implementação no Vue:  
No Vue, podemos usar o `watch` ou `watchEffect` para observar uma mudança de estado e disparar ações:

```javascript
// store/messages.js usando Pinia
import { defineStore } from 'pinia';

export const useMessageStore = defineStore('messages', {
  state: () => ({
    messages: [],
  }),
  actions: {
    addMessage(newMessage) {
      this.messages.push(newMessage);
    },
  },
});
```  
Em cada componente que precisa ser notificado de novas mensagens, podemos observar o `messages`:

```javascript
<script setup>
import { computed, watch } from 'vue';
import { useMessageStore } from './store/messages';

const messageStore = useMessageStore();
const messages = computed(() => messageStore.messages);

watch(messages, (newMessages) => {
  console.log('Nova mensagem recebida:', newMessages);
});
</script>
```  
Aqui, watch é o "Observador", e o estado messages é o "Sujeito". Quando o estado messages muda, todos os componentes que estão observando essa propriedade serão notificados.

[Voltar](../DesignPatterns.md)
