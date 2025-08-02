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
// import k nói làm gì đúng hong
import { onMounted, ref, watch } from 'vue';

// đặt 3 biến với giá trị mặc định, list to select là 1 ref kiểu mảng
const selectedId = ref('');
const listToSelect = ref([]);
const selectedObject = ref('');

// hàm này chạy khi bật web để lấy danh sách id | name của users để hiển thị lên select, async await tikitaka với nhau để múa lửa 
const getParentSelectBox = async() => {
    // thằng res chờ fetch users để gán giá trị vào nó
    const res = await fetch('https://jsonplaceholder.typicode.com/users');
    
    // thằng arrays chờ công việc res.json() đồng nghĩa với việc chờ nó biến thành 1 cục json
    const arrays = await res.json();
    
    // gán giá trị vào listToSelect, ở đây vì listToSelect là 1 ref nên gán giá trị phải dùng `.value`
    listToSelect.value = arrays
}

// onMounted này chạy khi vào web
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