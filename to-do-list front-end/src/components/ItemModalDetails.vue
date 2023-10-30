<template>
    <div class="fixed top-0 left-0 right-0 bottom-0 bg-black/40 w-screen h-screen flex justify-center items-center">
        <div class="w-[650px] h-[350px] bg-[#335642] rounded-lg px-5 py-3">
            <h1 class="text-gray-300">Tarefa #{{ item.id }}</h1>
            <textarea v-model="item.name" class="w-[100%] rounded-lg bg-[#223329] px-5 py-3 scroll_pattern focus:outline-none resize-none text-gray-500 focus:text-white" name="" id="" cols="20" rows="8"></textarea>
            <div class="h-[20%] flex justify-between items-center gap-3">
                <div class="flex flex-col">
                    <h1>Criado em: {{ item.created_at.substring(0, 10) }}</h1>
                    <h1>Completado em: <span v-if="item.completed_at">{{ item.completed_at.substring(0, 10) }}</span></h1>
                </div>
                <div class="flex gap-3">
                    <button @click="saveItemChange()" class="bg-red-700 rounded-lg px-5 py-2 hover:bg-red-900 transition-color">Save Edit</button>
                    <button @click="closePopup()" class="bg-[#292929] rounded-lg px-5 py-2 hover:bg-[#131313] transition-colors">Close Button</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script lang="ts">
import axios from 'axios';
import { defineComponent } from 'vue';
export default defineComponent({
    name: 'ItemModalDetails',
    props: ["item"],
    methods: {
        closePopup() {
            this.$emit("closePopup");
        },
        saveItemChange() {
            axios.put("http://127.0.0.1:8000/api/item/edit/" + this.item.id, {
                item: this.item
            }).then(response => {
                if (response.status == 200) {
                    this.$emit("itemchanged")
                    this.$emit("closePopup")
                }
            }).catch(error => {
                console.log(error);
            });
        }
    }
})
</script>

<style>
.scroll_pattern::-webkit-scrollbar {
  width: 10px;
}

/* Track */
.scroll_pattern::-webkit-scrollbar-track {
  background: #223329;
}

/* Handle */
.scroll_pattern::-webkit-scrollbar-thumb {
  background: #294937;
  border-radius: 4px;
}

/* Handle on hover */
.scroll_pattern::-webkit-scrollbar-thumb:hover {
  background: #555;
  cursor: pointer;
}

</style>