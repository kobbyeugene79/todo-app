<template>
  <div class="container">

    <div class="title">
        <h1 class="title__h1">Todo <span>App</span></h1>
      </div>
   
    <form @submit.prevent class="form">
      <div class="inputs">
        <h2 class="inputs__actions">Actions</h2>
        <input class="input-text" 
          v-model="newTodo" type="text" 
          name="new-todo" id="NewTodo" 
          placeholder="Enter new todo"
          autocomplete="off"
          >
        <button 
          class="btn"
          type="submit" 
          :disabled="newTodo.length === 0 || todos.length > 11"
          @click="addTodo"
          >
          Add todo
        </button>


        <div class="delTask">
          <input 
            v-model="numToDel" 
            type="text" 
            id="delByNum"
            class="input-text"
            autocomplete="off"
            placeholder="Enter index of task to delete"
            >
          <button 
            @click="delTodo" 
            :disabled="numToDel.length === 0"
            class="btn btn--del"
            >Delete
          </button>
        </div>
      </div>

      <div class="list">
        <h2 class="list__lists">My Tasks</h2>
        <ul class="list__menu">
          <li class="list__menu__item" 
            v-for="todo in todos" 
            :key="todo.id"
            >
            {{ todo.text }} 
          </li>
        </ul>
      </div>


    </form>

  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const todos = ref([
  {
    id: 0,
    text: 'i will go to school'
  },
  {
    id: 1,
    text: 'i will go to church'
  },
  {
    id: 2,
    text: 'i will go home'
  },
  {
    id: 3,
    text: 'i will do my homework'
  }
])

const numToDel = ref('')
const newTodo = ref('')

const addTodo = ()=>{
  if (todos.value.length >= 11){
    alert('Please delete some tasks before adding a new one')
  } else{
    todos.value.push({id: todos.value.length + 1, text: newTodo.value})
    newTodo.value = ""
  }
}

const index = computed(() => Number(numToDel.value) - 1)



const delTodo = () =>{
  if (isNaN(index.value)){
    alert('Its not a number')
  } else if (todos.value.length < index.value){
    alert('Number of tasks are less than the input')
  } else{
    todos.value.splice(index.value, 1)
  }
}



</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
$primary-color: #af80e9;
$bg-color: #e3e9ff;
$heading-color: #ffffff;
$text-color: #adb6cd;
$btn-color: #2414d4f3;

.container{
  // background: linear-gradient(45deg, #7924e7e7, #3221ecf3);
  background: $bg-color;
  width: 100%;
  height: 100vh;
  position: relative;
  background-size: 300% 300%;
  backdrop-filter: blur(10px);
  animation: bg-changes 12s ease-in-out infinite;

  @keyframes bg-changes {
    0%{
      background-position: 0 50%;
    }
    50%{
      background-position: 100% 50%;
    }
    100%{
      background-position: 0 50%;
    }
  }
  .title{
    text-align: center;
    padding-top: 4rem;

      &__h1{
        font-size: 2.5rem;
        color: $text-color;

        span{
          color: $primary-color;
        }
      }
    }
  .form{
    width: max-content;
    height: max-content;
    display: flex;
    position: absolute;
    left: 50%;
    top: 50%;
    align-items: baseline;
    background: #ffffff;
    transform: translate(-50%, -50%);
    color: $text-color;
    padding: 50px;
    background-image: url("data:image/svg+xml,%3csvg width='100%25' height='100%25' xmlns='http://www.w3.org/2000/svg'%3e%3crect width='100%25' height='100%25' fill='none' stroke='black' stroke-width='10' stroke-dasharray='2%2c 8' stroke-dashoffset='0' stroke-linecap='butt'/%3e%3c/svg%3e");
    box-shadow: rgba(0, 41, 82, 0.2) 0px 8px 24px;

    .inputs{
      width: 50%;
      margin-right: 10px;
      padding: 10px;
      border-right: dashed 2px $primary-color;

      &__actions{
        color: $primary-color;
      }
      .input-text{
      outline: none;
      border: none;
      // background: white;
      width: 100%;
      height: 2rem;
      padding: 0.5rem;
      margin: 1.5rem 0;
      border-left: 1px solid $primary-color;
      transition: 0,4s border;
      transition-delay: 0.2s;
      // box-shadow: rgba(0, 41, 82, 0.2) 0px 8px 24px;

      &:focus{
        box-shadow: none;
        border-bottom: 1px solid $primary-color;
        border-left: none;
      }
      &::placeholder{
        font-size: 0.85rem;
        padding-left: 0.5rem;
        transition: 0.9s;
      }

      &:focus::placeholder{
          transform: translateX(2em);
          opacity: 0;
        }
      }

    .btn{
      width: 100%;
      padding: 0.5rem 1.2rem;
      outline: none;
      border: $btn-color;
      background: $btn-color;
      color: white;
      cursor: pointer;
      box-shadow: rgba(0, 41, 82, 0.2) 0px 8px 24px;
      transition: .5s;
     
        &--del{
          background: #f03f3f;
        }
        &:hover{
          box-shadow: none;
        }

        &:disabled{
          cursor: not-allowed;
          background: $text-color;
          border: 1px solid $text-color;
        }
        
      }
    }
    
    .list{
      margin-left: 20px;

      &__lists{
        color: $primary-color;
        margin-bottom: 1rem;
      }

      &__menu{
        margin-left: 10px;

        &__item{
          list-style-type: decimal;
          font-size: 0.9rem;
        }
      }
    }

    .delTask{
      margin-top: 2rem;
    }
  }
}
</style>
