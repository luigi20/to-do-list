<template>
    <div class="mt-4 pt-1 px-4 border-t-2 border-gray-400 w-[30.125rem] h-screen overflow-y-auto flex flex-col gap-2">
        <div v-for="(item, index) in items" :key="index">
            <Items-List :item="item" v-on:itemchanged="$emit('reloadlist')"/>
        </div>
    </div>
</template>

<script lang="ts">
import ItemsList from "./ItemsList.vue"
import { defineComponent } from 'vue';
export default defineComponent({
    name: 'ItemsListContainer',
    props: ['items'],
    components: {
        ItemsList
    }
})
</script>

<style>

</style>