Here's our template for our Todos component. We are using the v-bind here to give a key to each todo item. Since the todo items we passed from app into the Todos component each have an ID, we are using that as the key. v-for is essentially Vue's version of a for loop. In this loop, we render each todo item in our array of todos. So for each todo, we render our TodoItem component, which we are passing the todos array to. Emit allows us to send the event up from Todos to app. We are naming the event del-todo and passing up the id of the event we are attempting to delete to app.
<template>
    <div>
        <div v-bind:key="todo.id" v-for="todo in todos">
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" />
        </div>
    </div>
</template>

Here we're importing our TodoItem component, and listing it under components because TodoItem is to be rendered by Todos. Additionally, the props:["todos"] part is setting the props for our Todos component to be the array of todos that was passed from app.vue
<script>
import TodoItem from './TodoItem.vue';

export default {
    name: "Todos",
    components:{
        TodoItem
    },
    props: ["todos"]
}
</script>

Scoped styles only affect the component they are written in. Non scoped styles are gobal.
<style scoped>

</style>