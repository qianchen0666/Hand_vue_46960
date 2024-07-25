<script setup>
import {ref} from "vue";
import {dayjs, ElMessage, ElMessageBox} from 'element-plus'
import {nanoid} from "nanoid";


const list = ref([])

const input = ref('')

const doList =ref([])
const showCompletedTasks = ref(false)


const addTodo = () => {
  if (input.value.trim()) {
    console.log(input.value)
    list.value.unshift(
        {
          id: nanoid(),
          task: input.value,
          complete: false,
          taskDateTime: dayjs().format('YYYY-MM-DD HH:mm:ss'),})
    input.value = ''
    ElMessage({
      message: '添加成功',
      type: 'success',
    })

  } else {
    return ElMessage.error('输入不能为空，请重新输入')

  }}
  const completeItem = (index) => {
    list.value[index].complete = true;
    doList.value.push(list.value[index])
    list.value.splice(index, 1);
    ElMessage({
      message: '任务已完成',
      type: 'success',
    });
  };
const chageItem = (index) => {
  doList.value.push(list.value[index])
  list.value.splice(index, 1);
  ElMessage({
    message: '任务已完成',
    type: 'success',
  });
}

  const editItem = (index) => {
    const newItem = prompt('修改任务:', list.value[index].task);
    if (newItem !== null) {
      list.value[index].task = newItem;
      ElMessage({
        message: '任务已修改',
        type: 'warning',
      });
    }
  };



const deleteItem = (index) => {
  ElMessageBox.confirm('确定要删除这个任务吗?', '确认删除', {
    confirmButtonText: '确定',
    cancelButtonText: '取消',
    type: 'warning',
  }).then(() => {
    list.value.splice(index, 1);
    ElMessage({
      message: '任务已删除',
      type: 'success',
    });
  }).catch(() => {
    ElMessage({
      message: '取消删除',
      type: 'info',
    });
  });
};

const toggleCompletedTasks = () => {
  showCompletedTasks.value = !showCompletedTasks.value;
};

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
      <ul v-for=" (item, index) in list" :key="item.id" >
        <div class="item-container">
        <li>
          <el-checkbox v-model="item.complete"  @change="chageItem(index)">
            <el-input v-model="item.task" style="width: 240px" placeholder="Please input" />
            {{item.taskDateTime}}</el-checkbox>
        </li>
          <el-button type="text" @click="completeItem(index)">完成</el-button>
          <el-button type="text" @click="editItem(index)">修改</el-button>
          <el-button type="text" @click="deleteItem(index)">删除</el-button>
        </div>
      </ul>

  <el-button
      style="max-width: 600px"
      type="primary"
      round
      @click="toggleCompletedTasks"
  >
    {{ showCompletedTasks ? '点击隐藏已完成任务' : '点击显示已完成任务' }}
  </el-button>

  <ul v-if="showCompletedTasks">
    <li v-for="item in doList" :key="item.id">
      <div class="item-container">
        <el-checkbox v-model="item.complete" disabled>
          <el-input  v-model="item.task" style="width: 240px" disabled />
          {{ item.taskDateTime }}
        </el-checkbox>
      </div>
    </li>
  </ul>

</template>


<style scoped>
.item-container {
  display: flex;
  align-items: center; /* 垂直居中对齐 */
  gap: 10px; /* 调整间距 */
}
</style>