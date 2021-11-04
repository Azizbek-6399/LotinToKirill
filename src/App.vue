<template>
  <v-app>
    <List />
    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
import List from './components/List.vue'
  export default {
    name: "App",
    components:{
      List
    }
  };
</script>