*** Guia do Mochileiro VUE.JS ***

Arquivos: <p>
``App.vue:`` Componente pai que mantém o estado e a lógica.

A) O que é a função `defineProps`?<p>
r/ Ela serve para receber um objeto de um componente.
---
B) O que é `defineEmits`?<p>
r/ Faz a emissão de eventos, ex: toggle/delete.
---
🔹 Analogia

Pense assim:

TodoItem = modelo de cartão

App.vue = caixa que guarda os cartões reais

Você pode usar muitos cartões (componentes) a partir do mesmo modelo, mas só o pai decide quais existem, como mudam e quando somem.


            +-------------------+
            |      App.vue      |  <-- componente pai
            |-------------------|
            | data: todos[]     |  <-- lista de tarefas (estado central)
            | methods:          |
            | - addTodo         |
            | - handleToggle    |
            | - handleDelete    |
            +-------------------+
               |            |
        emit 'add'       passes props
               |            |
        +------+----+   +---+----------------+
        | TodoForm  |   |   TodoItem         |
        |-----------|   |-------------------|
        | input     |   | :todo (prop)      |
        | button    |   | @toggle / @delete |
        +-----------+   +-------------------+
               ^
               | emits 'add' (novo texto)
               |
        Atualiza todos[] no App.vue

🔹 Como ler esse esquema

1. App.vue tem o estado principal (todos[]) e métodos que manipulam a lista.


2. TodoForm é só o formulário:

Recebe input do usuário.

Emite add para o pai.



3. TodoItem é uma instância da tarefa:

Recebe todo via prop.

Emite toggle ou delete quando o usuário interage.



4. Tudo acontece no App.vue:

O pai atualiza todos[].

O Vue propaga automaticamente a mudança para os TodoItems na tela.