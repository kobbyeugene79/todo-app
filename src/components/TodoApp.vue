<template>
  <div class="container">

    <form @submit.prevent="addTodo" class="form">
      <input class="form__input-text" v-model="newTodo" type="text" name="new-todo" id="NewTodo" placeholder="Enter new todo">
      <button class="form__btn" type="submit">Add todo</button>

    <ul class="menu">
      <li class="menu__item" v-for="{text, id} in todos" :key="id">{{ text }}</li>
    </ul>
    </form>


  </div>
</template>

<script setup>
import { ref } from 'vue';

const todos = ref([
  {
    id: 'todo1',
    text: 'i will go to school'
  },
  {
    id: 'todo2',
    text: 'i will go to church'
  },
  {
    id: 'todo3',
    text: 'i will go home'
  },
  {
    id: 'todo4',
    text: 'i will do my homework'
  }
])


const newTodo = ref('')

const addTodo = ()=>{
  
  todos.value.push({id: todos.value.length + 1, text: newTodo.value})
  newTodo.value = ""
}

// const delTodo = () =>{
//   todos.value.pop()
// }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container{
  background: linear-gradient(to right bottom, white, lightblue);
  width: 100%;
  height: 100vh;
  position: relative;
  .form{
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    border: 1px solid red;
    padding: 50px;
    backdrop-filter: blur(10px);

    &__input-text{
      outline: none;
      border: none;
      background: white;
      width: 20em;
      height: 2rem;
      margin: 1.5rem 0;

      &::placeholder{
        color: gray;
        font-size: 1rem;
        transition: 0.9s;
      }

      &:focus::placeholder{
          transform: translateX(2em);
          opacity: 0;
        }
    }

    &__btn{
      padding: 0.5rem 1.2rem;
      outline: none;
      border: blue;
      background: blue;
      color: white;
      margin-left: 0.5rem;
      cursor: pointer;
        box-shadow: rgba(0, 41, 82, 0.2) 0px 8px 24px;
      transition: .5s;

      &:hover{
        box-shadow: none;
      }
    }
  }
}
</style>
