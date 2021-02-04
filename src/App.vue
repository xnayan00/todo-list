<template>
  <div id="app">
    <header>
      <div><i class="fas fa-thumbtack fa-xs mr-3"></i>Lista de Tarefas</div>
    </header>

    <div class="container">
      <div class="menu row justify-content-around my-5">
          <a href="javascript:void(0)" @click="currentListButton">Início</a>
          <a href="javascript:void(0)" @click="completedListButton">Tarefas Concluídas</a>
          <a href="javascript:void(0)" @click="removedListButton">Tarefas Excluídas</a>   
      </div>

      <div class="row content">   

        <div class="col-md-8">
          <div class="mb-4">
            <h3>{{ sectionTitle }}</h3>
            <div class="custom-hr"></div>
          </div>

          <ul v-if="completedList === true">
              <li class="list-unstyled"
                  v-for="(completedTask, index) in completedTasks"
                  :key="index">
                  {{ completedTask.title }}
                  <hr>                        
              </li>                    
          </ul>

          <ul v-else-if="removedList === true">
              <li class="list-unstyled"
                  v-for="(removedTask, index) in removedTasks"
                  :key="index">
                  {{ removedTask.title }}
                  <hr>                        
              </li>                    
          </ul>

          <TaskList
            v-else
            v-for="(task, index) in currentTasks"
            :key="index"
            :task="task"
            @completeTask="completeTask(task)"
            @removeTask="removeTask(task)"
          />

          
        </div>

          <AddTask 
            v-if="newTaskPanel === true"            
            @addTask="addTask"
          />

      </div>

    </div>
   
  </div>      
</template>

<script>

import TaskList from './components/taskList'
import AddTask from './components/addTask'

export default {
  components:{
    TaskList,
    AddTask
  },

  data(){
    return {
      tasks: [],
      sectionTitle: 'Suas Tarefas',
      removedList: false,
      completedList: false,
      newTaskPanel: true
      
    }
  },
  methods: {
    addTask(title){
      this.tasks.push({id: this.tasks.length + 1, title: title, completed: false, removed: false }) 
    },
    completeTask(task){
      task.completed = true
      console.log(task)
    },
    removeTask(task){
      task.removed = true
      console.log(task)
    },
    currentListButton(){
      this.removedList = false
      this.completedList = false
      this.newTaskPanel = true
      this.sectionTitle = 'Suas Tarefas'
    },
    removedListButton(){
      this.removedList = true
      this.completedList = false
      this.newTaskPanel = false
      this.sectionTitle = 'Tarefas Removidas'
    },
    completedListButton(){
      this.removedList = false
      this.completedList = true
      this.newTaskPanel = false
      this.sectionTitle = 'Tarefas Concluídas'
    }
  },
  computed: {
      currentTasks(){
          return this.tasks.filter(function(value){
              return value.removed === false && value.completed === false
          })
      },
      removedTasks(){
          return this.tasks.filter(function(value){
                return value.removed === true
          })
      },
      completedTasks(){
          return this.tasks.filter(function(value){
                return value.completed === true
          })
      }
  }

}
</script>

<!--Custom Style-->
<style lang="css"> 
  :root{
    --primary-color: rgb(29, 201, 143);
    --danger-color: rgb(201, 55, 29);
    --warning-color: rgb(201, 141, 29);
    --info-color: rgb(88, 101, 107);
    --dark-color: rgb(17, 25, 29);
  }

header {
  background-color: var(--primary-color);
  padding: 20px;
  color: #fff;
  text-align: center;
  font-size: 1.5em;
  font-weight: bold;
}

h3 {
  font-weight: 600;
  color: var(--info-color);
}

ul {
  list-style: none;
}

a.new-task-btn {
  color: #fff;
  background-color: var(--primary-color);
  font-weight: 600;
  border-radius: 50px;
  padding: 10px;
}

a.new-task-btn:hover {
  text-decoration: none;
}

.actions {
  display: inline;
}

.content {
  border: 1px solid rgb(212, 211, 211);
  border-radius: 20px;
  padding: 30px;
}

.custom-hr {
  background-color: var(--primary-color);
  width: 70px;
  height: 7px;
}

.menu {
  padding: 0px 200px;
}

.menu a {
  padding: 10px;
  width: 200px;
  border-radius: 50px;  
  color: var(--info-color);
  background-color: #fff;
  border: 2px solid var(--primary-color);
  text-align: center;
  font-weight: 700;
  transition: background-color 0.2s, color 0.2s;
}

.menu a:hover {
  background-color: var(--primary-color);
  color: #fff;
  text-decoration: none;
}

</style>


