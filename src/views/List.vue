<!-- Home.vue -->
<template>
  <div class="todoList">
    <header>
      <section>
        <h1>My To-Do List</h1>
        <input type="text" v-model="todo" @keyup.enter="addTodo" placeholder="加入ToDo" />
      </section>
    </header>
    <section class="items">
      <h2 class="pending">待辦中<span class="badge">{{todoList.length}}</span></h2>
      <h2 class="done">已完成<span class="badge">{{doneList.length}}</span></h2>
      <label v-for="(item, index) in allList" :key="'info-'+ index" :class="{ isDone: item.done }">
        <input type="checkbox" @change="changeTodo(item)">
        <span>{{item.todo}}</span>
        <a @click="deleteTodo(index,true)">-</a>
      </label>
    </section>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        todo: '',
        allList: [
          {
            todo: '刷牙',
            done: false
          }
        ],
        todoLen: 1
      }
    },
    methods: {
      addTodo () {
        let todoObj = {
          todo: this.todo,
          done: false
        };
        this.allList.push(todoObj);
        this.todo = '';
      },
      changeTodo (item) {
        item.done=!(item.done);
        console.log(item);
      },
      deleteTodo (index, done) {
        if(done){
          this.todoLen--;
        }
        this.allList.splice(index, 1);
      },
    },
    computed: {
      todoList (){
        return this.allList.filter(child => !child.done);
      },
      doneList (){
        return this.allList.filter(child => child.done);
      }
    }
  }
</script>