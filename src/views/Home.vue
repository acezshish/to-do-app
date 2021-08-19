<template>
  <div class="home">
    <v-text-field
      v-model="newtasktitle"
      @click:append="addTask"
      @keyup.enter="addTask"
      class="pa-3"
      outlined
      label="Add Task"
      prepend-icon="mdi-plus"
      hide-details=""
      clearable
    ></v-text-field>

    <v-list> </v-list>

    <v-divider></v-divider>

    <v-list flat subheader three-line>
      <v-list-item
        @click="donetask(task.id)"
        :class="{ 'blue lighten-5': task.done }"
        v-for="task in tasks"
        :key="task.id"
      >
        <template v-slot:default="{}">
          <v-list-item-action>
            <v-checkbox :input-value="task.done"></v-checkbox>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title
              :class="{ 'text-decoration-line-through': task.done }"
              >{{ task.title }}</v-list-item-title
            >
          </v-list-item-content>
          <v-list-item-action>
            <v-btn @click.stop="deleteTask(task.id)">
              <v-icon color="grey lighten-1">mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
        </template>
      </v-list-item>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      newtasktitle: "",
      tasks: [
        {
          id: 1,
          title: "Wake up",
          done: false,
        },
        {
          id: 2,
          title: "Have Breakfast",
          done: false,
        },
        {
          id: 3,
          title: "Go to Work",
          done: false,
        },
      ],
    };
  },
  methods: {
    addTask() {
      let newTask = {
        id: Date.now(),
        title: this.newtasktitle,
        done: false,
      };
      this.tasks.push(newTask);
      this.newtasktitle = "";
    },
    donetask(id) {
      let task = this.tasks.filter((task) => task.id == id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
  },
};
</script>
