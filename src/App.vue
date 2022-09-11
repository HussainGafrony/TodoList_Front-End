<template>
  <v-app>

    <h2> Todo List</h2>
    <AddTodo @add-todo="gitTodo()"></AddTodo>
    <ShowTodo :item="items"  @delete-todo="gitTodo()"></ShowTodo>

  </v-app>
</template>

<script>
import AddTodo from '@/components/AddTodo.vue';
import ShowTodo from '@/components/ShowTodo.vue';
import axios from 'axios';
export default {
  name: 'App_',
  components: { AddTodo,ShowTodo },
  data: () => ({
    items: [],
  }),
  methods: {
    gitTodo() {
      axios.get("http://127.0.0.1:8000/api/items").then((response) => {
        this.items = response.data;
      }).catch((error) => {
        console.log(error);
      })
    }
  },
  created(){
    this.gitTodo();
  },
};
</script>

<style scoped>
body {
  background: #e6e6e6;
}

h2 {
  padding-top: 45px;
  font-size: 40px;
  align-content: center;
  text-align: center;

}
</style>
