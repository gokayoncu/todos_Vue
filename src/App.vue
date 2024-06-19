<script>
import {ref} from "vue"
export default{
  setup(){
    const todo= ref("");
    const newTodo= ref("");
    const todos= ref([]);
    const edit = ref(false)
    const editId=ref()
    const addTodo= ()=>{
      let random= Math.floor(Math.random()*100);
      todos.value.push({
        done:false,
        content:todo.value,
        id: random
      });
      todo.value = "";
    }
    const editTodo=()=>{
      const filterTodo = todos.value.find((todo)=>todo.id === editId.value)
      console.log(filterTodo)
    }
    const todoEdit =(id)=>{
      edit.value = true;
      editId.value=id
    }
    const deleteTodo=(id)=>{
      const deletetodos = todos.value.filter((todo)=>todo.id != id)
      todos.value= deletetodos;
    }
    const completed =(todo)=>{
      todo.done=!todo.done;
    }

    return{todo, todos, addTodo,deleteTodo,completed,todoEdit,edit,editTodo,newTodo}
  }
}
</script>

<template>
  <div class="container">
    <h2>Todos App</h2>
    <div class="add-todo">
      <input type="text" v-model="todo" placeholder="Todo Enter" style="width: 500px;border-radius: 10px;padding-left: 10px;height: 30px;">
      <button @click.prevent="addTodo" style="background-color: rgb(12, 162, 216);color: white;border-radius: 10px">Submit</button>
    </div>
    <div class="todos">
      <div v-for="todo in todos" :key="todo.id" class="todos-content">
        <span :class="{completed:todo.done}">{{ todo.content }}</span>
        <div style="display: flex;gap: 1rem;">
          <svg @click.prevent="()=>deleteTodo(todo.id)" style="cursor: pointer;" stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 24 24" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path fill="none" d="M0 0h24v24H0V0z"></path><path d="M16 9v10H8V9h8m-1.5-6h-5l-1 1H5v2h14V4h-3.5l-1-1zM18 7H6v12c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7z"></path></svg>
          <svg @click.prevent="todoEdit(todo.id)" style="cursor: pointer;" stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 24 24" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><g id="Edit"><g><path d="M3.548,20.938h16.9a.5.5,0,0,0,0-1H3.548a.5.5,0,0,0,0,1Z"></path><path d="M9.71,17.18a2.587,2.587,0,0,0,1.12-.65l9.54-9.54a1.75,1.75,0,0,0,0-2.47l-.94-.93a1.788,1.788,0,0,0-2.47,0L7.42,13.12a2.473,2.473,0,0,0-.64,1.12L6.04,17a.737.737,0,0,0,.19.72.767.767,0,0,0,.53.22Zm.41-1.36a1.468,1.468,0,0,1-.67.39l-.97.26-1-1,.26-.97a1.521,1.521,0,0,1,.39-.67l.38-.37,1.99,1.99Zm1.09-1.08L9.22,12.75l6.73-6.73,1.99,1.99Zm8.45-8.45L18.65,7.3,16.66,5.31l1.01-1.02a.748.748,0,0,1,1.06,0l.93.94A.754.754,0,0,1,19.66,6.29Z"></path></g></g></svg>
          <svg @click.prevent="completed(todo)" :class="{completed:todo.done}" style="cursor: pointer;" stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 24 24" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M21.03 5.72a.75.75 0 0 1 0 1.06l-11.5 11.5a.747.747 0 0 1-1.072-.012l-5.5-5.75a.75.75 0 1 1 1.084-1.036l4.97 5.195L19.97 5.72a.75.75 0 0 1 1.06 0Z"></path></svg>
        </div>
      </div>
    </div>
    <div v-if="edit" class="editPage">
        <input type="text" v-model="newTodo" placeholder="Edit" style="width: 500px;border-radius: 10px;padding-left: 10px;height: 30px;">
        <button @click.prevent="editTodo(todo)" style="background-color: rgb(12, 162, 216);color: white;border-radius: 10px;height: 30px;">Submit</button>
    </div>
  </div>
</template>

<style scoped>
  #app{
    margin: 0;
    padding: 0;
  }
  .todos{
    display: flex;
    flex-direction: column;
  }
  .todos-content{
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #ccc;
  }
  .add-todo{
    display: flex;
    gap: 2rem;
    padding-top: 2rem;
    
  }
  .completed{
    color: rgb(18, 212, 18);
    text-decoration: line-through;
    text-decoration-color: #000;
  }
  .editPage{
    display: flex;
    gap: 1rem;
    align-items: center;
    justify-content: center;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(212, 212, 212, 1);
  }
</style>
