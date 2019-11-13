Here, we've got our template which is rendering each todo title. The todo is coming from the array pssed from App to Todos to TodoItem. Here, we are using v-bind to bind a class on a condition. Here, we are telling our div that if the todo is completed, the todo should have the class "is-complete". the todo.completed is the condition. If completed is true, that todo will get the class is-complete. Our input is creating a checkbox. v-on:change is essentially onChange, similar to onClick. We are telling our app that when the input changes, it should markComplete. Remember, because Todos is looping through each TodoItem by key, this will be rendered 3 times as there are 3 Todo Items. The @click is essentially the same as v-on:click. Our array is up on the app level. So we can't delete from TodoItem. When we use emit, that allows us to pass an event up from TodoItem to Todos. del-todo is the name of our event. todo.id is a parameter, passing that up tells Todos what we are deleting. This still needs to be passed from Todos to App
<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <p>
            <input type="checkbox" v-on:change="markComplete">{{ todo.title }}
            <button @click="$emit('del-todo', todo.id)" class="del">x</button></p>
    </div>
</template>
We can add methods to a component the same way we add props to it. Check out how we add markComplete. When called, the method checks the state of whether the todo is completed and changes it to the opposite of it's current state.
<script>
export default {
    name: "TodoItem",
    props: ["todo"],
    methods:{
        markComplete(){
            this.todo.completed = !this.todo.completed
            }
        }
}
</script>

<style scoped>
    .todo-item{
        background: #f4f4f4;
        padding:10px;
        border-bottom:apx #ccc dotted
    }

    .is-complete {
        text-decoration: line-through;
    }

    .del {
        background: #ff0000;
        color:#fff;
        border:none;
        padding:5px 9px;
        border-radius:50%;
        cursor: pointer;
        float: right;
    }
</style>