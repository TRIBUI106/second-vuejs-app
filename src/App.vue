<template>

    <label for="" class="form-label">Chọn đi</label>
    <select class="form-select" v-model="selectedId">
        <option :value="item.id" class="" v-for="item in listToSelect" >{{ item.id }} | {{ item.name }}</option>
    </select>
    <div class="mt-5 h1">
        {{ selectedObject.id }}
        <br>
        {{ selectedObject.name }}
        <br>
        {{ selectedObject.website }}
    </div>
  
</template>

<script setup>
import { onMounted, ref, watch } from 'vue';

const selectedId = ref('');
const listToSelect = ref([]);
const selectedObject = ref('');

const getParentSelectBox = async() => {
    const res = await fetch('https://jsonplaceholder.typicode.com/users');
    const arrays = await res.json();
    listToSelect.value = arrays
}

onMounted(() => {
    getParentSelectBox();
    selectedId.value = listToSelect[0].value;
})

watch(selectedId, async (newVal) => {

    const res = await fetch(`https://jsonplaceholder.typicode.com/users/${newVal}`);
    const object = await res.json();
    selectedObject.value = object;

})

</script>