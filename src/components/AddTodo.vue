v-model "title" tells us that the text put into the input can be stored in the data under "title". The @submit part tells us that when the form is submitted we will call the method "addTodo".

<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" name="title" placeholder="Add Todo...">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>
If we want our form to do anything when submitted fields must be added to data for the component. Since we are adding a "title" fo the Todo, we must put it in data. uuid is a package we imported that generates a unique ID, in this case when we add an event.
<script>
import uuid from 'uuid';
export default {
    name: "AddTodo",
    data(){
        return {
            title: ''
        }
    },
    methods: {
        addTodo(evt){
            //Our method addtodo creates a newTodo. It assigns the id to a random id utilizing our uuid plugin, it sets the title to this.title, which is gathered via the input field, and sets completed to false.
            evt.preventDefault();
            const newTodo = {
                id: uuid.v4(),
                title: this.title,
                completed:false
            };
            //The emit part sends the add-todo event up to the parent component, using the newTodo as a parameter.
            this.$emit('add-todo', newTodo);
            //This.title clears the form
            this.title=""
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
        }

    input[type="text"] {
        flex: 10; 
        padding: 5px;
        }
    input[type="submit"] {
        flex: 2;
    }
</style>