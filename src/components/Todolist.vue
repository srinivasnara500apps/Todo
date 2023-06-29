<script setup>
import { ref, reactive, computed, watch } from 'vue'
import cookie from "./cookie.vue"

const names = reactive(['Rohit Sharma','Shubman Gill', 'Virat Kohli','Rishab Pant']) 
const Array=ref([])
const selected = ref('')
const prefix = ref('')
const first = ref('')
const updatestroage=()=>{
        localStorage.setItem("names", JSON.stringify(names))
}
const filteredNames = computed(() =>
  names.filter((n) =>
    n.toLowerCase().startsWith(prefix.value.toLowerCase())
  )
)
watch(selected, (name) => {
  ;[first.value] = name.split(', ')
})
function create() {
  if (first.value.trim()!=="") {
    if (!names.includes(first.value)) {  
      names.push(first.value)
      first.value = ''

     }
  }
  updatestroage()
}
function update() {
  if (first.value.trim() && selected.value) {
    const i = names.indexOf(selected.value)
    names[i] = selected.value = `${first.value}`  
    selected.value = first.value = ''
  }
  updatestroage()
}
function del() {
  if (selected.value) {
    const i = names.indexOf(selected.value)
  let Strings=  names.splice(i, 1)
  Strings.forEach(item=>{
    Array.value.push(item)
  })
        sessionStorage.setItem("names", JSON.stringify(Array.value))

    selected.value = first.value = ''
  }
}
</script>
<template>
  <center><br><br><div class="run" ><br>
  <div><input  type="text" id="small-input" class="block w-full p-2 text-gray-900 border border-gray-600 rounded-lg bg-purple-50 sm:text-xs  focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="prefix" placeholder="Filter prefix"></div>
  <select size="6" class="bg-blue-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="selected">
    <option class="text-red-600" v-for="name in filteredNames" :key="name">{{ name }}</option>
  </select>
  <label class="text-yellow-600">Name: <input  type="text" id="small-input" class="block w-full p-2 text-gray-900 border border-gray-600 rounded-lg bg-purple-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="first"></label>
  <div class="buttons">
    <button class="bg-cyan-500 hover:bg-cyan-600 ..." @click="create">Create</button>
    <button class="bg-orange-500 hover:bg-orange-700 ..." @click="update">Update</button>
    <button class="bg-indigo-500 hover:bg-indigo-700 ..." @click="del">Delete</button>
  </div><hr><br>
  <cookie/>
</div></center>
</template>

<style>
* {
  font-size: inherit;
} 
.run{
  height: 400px;
  width: 500px;
  border: solid grey;
}

input {
  margin-bottom: 15px;
}

select {
  margin-bottom: 15px;
}
button + button {
  margin-left: 15px;
}
</style>

