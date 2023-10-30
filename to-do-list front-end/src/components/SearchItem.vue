<template>
    <input v-model="item.name" v-on:keyup.enter="addItem"
        class="bg-[#223329] w-[28.125rem] py-[10px] px-[10px] rounded-md text-white" type="text"
        placeholder="Crie suas tarefas">
</template>

<script lang="ts">
import axios from 'axios';
import { defineComponent } from 'vue';
export default defineComponent({
    name: 'SearchItem',
    data: function () {
        return {
            item: {
                name: ""
            }
        }
    },
    methods: {
        addItem() {
            if (this.item.name == "") {
                return;
            }
            axios.post('http://127.0.0.1:8000/api/item/store', {
                item: this.item
            })
                .then(response => {
                    if (response.status == 201) {
                        this.item.name == "";
                        this.$emit('reloadlist');
                    }
                })
                .catch(error => {
                    console.log(error);
                })
        }
    },
})
</script>