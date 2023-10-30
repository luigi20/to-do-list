
<template>
  <main class="w-screen h-screen bg-[#1E1E1E] flex justify-center">
    <div
      class="bg-[#335642] w-[35.125rem] h-[48.187rem] rounded-[50px] flex flex-col items-center shadow_pattern mt-16 py-5 px-4">
      <h1 class="text-[27px] font-semibold text-white">To-do-List</h1>
      <SearchItem v-on:reloadlist="getListItems()"/>
      <!-- parte das tarefas -->
      <ItemsListContainer :items="items" v-on:reloadlist="getListItems()"/>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from "axios";

/* Componentes do projeto */
import SearchItem from "./components/SearchItem.vue";
import ItemsListContainer from "./components/ItemsListContainer.vue";
import ItemModalDetails from './components/ItemModalDetails.vue';
export default defineComponent({
  name: 'App',
  components: {
    SearchItem,
    ItemsListContainer,
    ItemModalDetails
},
  data: function () {
    return {
      items: []
    }
  },
  methods: {
    getListItems () {
      axios.get('http://127.0.0.1:8000/api/items').then(response => {
        this.items = response.data
      }).
      catch(error => {
        console.log( error );
      })
    }
  },
  created() {
    this.getListItems();
  }
})
</script>


<style scoped>
.shadow_pattern {
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}
</style>
