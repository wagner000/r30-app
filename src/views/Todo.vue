<template>
  <div class="home">

    <v-text-field
      v-model="newTaskTtile"
      @click:append="addTask"
      @keyup.enter="addTask"
      hide-details
      clearable
      class="pa-3"
      outlined
      label="Add Task"
      append-icon="mdi-plus">
    </v-text-field>

    <v-list flat class="pt-0">
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'blue darken-4': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done }"
              >
                {{ task.title }}
              </v-list-item-title>
              <v-list-item-subtitle>Allow notifications</v-list-item-subtitle>
            </v-list-item-content>

            <v-list-item-action>
              <v-btn
                @click.stop="deleteTask(task.id)"
                icon>
                <v-icon color="primary">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  data() {
    return {
      newTaskTtile: '',
      tasks: [
        {
          id: 1,
          title: "Acordar",
          done: false,
        },
        {
          id: 2,
          title: "Fazer Café",
          done: false,
        },
        {
          id: 3,
          title: "Trabalhar",
          done: false,
        },
      ],
    };
  },
  methods: {
    doneTask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id){
      this.tasks = this.tasks.filter(task => task.id !== id)
    },
    addTask(){
      let newTask = {
        id: Date.now(),
        title: this.newTaskTtile,
        done: false
      }
      this.tasks.push(newTask)
      this.newTaskTtile = ''
    }
  },
};
</script>
