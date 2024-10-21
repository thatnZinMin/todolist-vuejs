<template>
  <body>
    <section class="w-full min-h-screen px-4 min-w-full">
      <h1 class="text-5xl pt-20 font-bold flex justify-center text-slate-100 ">To-Do-List</h1>
      <div class="container mx-auto p-6 md:p-12 lg:p-24">
       
          <div class="flex flex-col md:flex-row mb-4">
          <input
            v-model="newTask"
            type="text"
            placeholder="Add a new task"
            class="border border-color: rgb(3 105 161) rounded p-2 w-full md:w-5/6 shadow-lg shadow-gray-500/100"
          />
          <button
            @click="addTask"
            class="mt-2 md:mt-0 md:ml-2 bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-900 duration-300 shadow-lg shadow-blue-500/50"
          >
            Add Task
          </button>
        </div>
    
        
           <ul class="list-none pt-10 grid gap-4">
          <li 
            v-for="(task, index) in tasks"
            :key="index"
            class="flex flex-col md:flex-row md:justify-between md:gap-4"
          >
            
               <span class="w-full md:w-5/6 text-lg bg-blue-900 text-white px-4 py-2 rounded">   
              <div v-if="task.isEditing" class="flex gap-4">
               
                <input
                  v-model="task.title"
                  type="text"
                  class="w-full p-1 text-black rounded"
                />
                   <button @click="saveTask(index)" class="ml-2 bg-green-500 text-white px-4 py-2 rounded">
                  Save
                </button>
              </div>  
                 <div v-else>
            
                {{ task.title }}
              </div>
            </span>
            <div class="flex gap-2">
              <button
                v-if="!task.isEditing"
                @click="editTask(index)"
                class="bg-blue-500 text-white px-4 py-2 rounded"
              >
                Edit
              </button>
              <button
                @click="deleteTask(index)"
                class="bg-red-500 text-white px-4 py-2 rounded"
              >
                Delete
              </button>
            </div>
          </li>
        </ul>
      </div>
    </section>
  </body>
</template>

<script>
export default {
  data() {
     return {
      newTask: '',              
      tasks: [
         { title: 'todolist project use vue.js and tailwind', completed: false, isEditing: false },
        { title: 'create Thant Zin Min 2024', completed: false, isEditing: false }
      ]
    };
  },
  methods: {
    toggleComplete(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
      editTask(index) {
    
      this.tasks[index].isEditing = true;
    },
     saveTask(index) {
    
      this.tasks[index].isEditing = false;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    addTask() {
        if (this.newTask.trim() !== '') {
        this.tasks.push({
          title: this.newTask,
          completed: false,
          isEditing: false
        });
        this.newTask = ''; 
      }
    }
  }
};
</script>

<style scoped>
.line-through {
  text-decoration: line-through;
}
* {
  margin: 0 auto;
  padding: 0 auto;
  box-sizing: border-box;
}
body {
  background: linear-gradient(to top right, #000, #304156);
}
</style>
