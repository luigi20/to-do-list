<template>
    <div class="border-b-2 border-gray-400 flex items-center justify-between py-2">
        <ItemModalDetails :item="item" v-if="showPopup" :show="showPopup" v-on:closePopup="closePopup()"
            v-on:itemchanged="$emit('itemchanged')" />
        <div class="flex items-center gap-2">
            <input type="checkbox" :checked="completed" @change="updateCheck()">
            <h1 @click="showPopup = true"
                :class="[item.completed ? 'line-through text-gray-500' : '', 'w-[390px] truncate cursor-pointer hover:underline']">{{ item.name }}</h1>
        </div>
        <button @click="removeItem()"
            class="group w-7 h-7 rounded-sm flex items-center justify-center bg-[#223329] hover:bg-[#18241d]">
            <i class="fa-regular fa-trash-can text-red-500 group-hover:text-red-700 transition-colors"></i>
        </button>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import axios from "axios";
import ItemModalDetails from './ItemModalDetails.vue';
export default defineComponent({
    name: "ItemsList",
    props: ["item"],
    computed: {
        completed(): any {
            return Boolean(this.item.completed);
        }
    },
    data() {
        return {
            showPopup: false,
        }
    },
    methods: {
        closePopup() {
            this.showPopup = false;
        },
        updateCheck() {
            this.item.completed = !this.item.completed;
            axios.put("http://127.0.0.1:8000/api/item/" + this.item.id, {
                item: this.item
            }).then(response => {
                if (response.status == 200) {
                    this.$emit("itemchanged");
                }
            }).catch(error => {
                console.log(error);
            });
        },
        removeItem() {
            axios.delete("http://127.0.0.1:8000/api/item/" + this.item.id).then(response => {
                if (response.status == 200) {
                    this.$emit("itemchanged");
                }
            }).catch(error => {
                console.log(error);
            });
        },
    },
    components: { ItemModalDetails }
})
</script>