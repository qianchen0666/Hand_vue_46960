<script setup>
import {ref} from "vue";
import {ElMessage} from 'element-plus'



const list = ref([])

const input = ref('')


const addTodo = () => {
  if (input.value.trim()) {
    console.log(input.value)
    list.value.unshift(
        {
          id: "",
          task: input.value,
          complete: false})
    input.value = ''
    ElMessage({
      message: '添加成功',
      type: 'success',
    })

  } else {
    return ElMessage.error('输入不能为空，请重新输入')

  }
  // const completeItem = (index) => {
  //   // Logic to mark the item as complete
  //   console.log(`Item ${index} marked as complete`);
  // };
  //
  // const editItem = (index) => {
  //   // Logic to edit the item
  //   const newItem = prompt('Edit item:', list.value[index]);
  //   if (newItem !== null) {
  //     list.value.splice(index, 1, newItem);
  //   }
  // };
  //
  // const deleteItem = (index) => {
  //   list.value.splice(index, 1);
  // };


}


</script>

<template>
  <div>
    <el-input
        v-model="input"
        style="max-width: 600px"
        placeholder="添加todo"
        clearable
        @keyup.enter="addTodo"
    >
      <template #prepend>＋todolist</template>
    </el-input>
  </div >


      <ul v-for="item in list" :key="item" >

        <div class="item-container">
        <li>
          <el-checkbox v-model="item.task">{{item.task}}</el-checkbox>
        </li>
        </div>
      </ul>

      <el-button type="text" @click="list.splice(list.indexOf(item), 1)">删除</el-button>
      <el-button type="text" @click="completeItem(index)">完成</el-button>
      <el-button type="text" @click="editItem(index)">修改</el-button>
      <el-button type="text" @click="deleteItem(index)">删除</el-button>




</template>


<style scoped>
.item-container {
  display: flex;
  align-items: center; /* 垂直居中对齐 */
  gap: 10px; /* 调整间距 */
}
</style>