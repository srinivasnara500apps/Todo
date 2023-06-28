<script setup>
import { ref, reactive, computed, watch } from 'vue'

const names = reactive(['Nara Bannu', 'Kohli Virat']) 
const Array=ref([])
const selected = ref('')
const prefix = ref('')
const first = ref('')
// const last = ref('')

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
    // const fullName = `${last.value}, ${first.value}`
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
  }
  updatestroage()
}
// const updatestroages=()=>{
//   sessionStorage.getItem("names")
// }


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
  // updatestroages()
}
</script>

<template>
  <center><br><br><div class="run"><br>
  <div><input  type="text" id="small-input" class="block w-full p-2 text-gray-900 border border-gray-600 rounded-lg bg-purple-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="prefix" placeholder="Filter prefix"></div>
  <select size="6" class="bg-blue-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="selected">
    <option v-for="name in filteredNames" :key="name">{{ name }}</option>
  </select>

  <label>Name: <input type="text" id="small-input" class="block w-full p-2 text-gray-900 border border-gray-600 rounded-lg bg-purple-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="first"></label>
  <!-- <label>Surname: <input type="text" id="small-input" class="block w-full p-2 text-gray-900 border border-gray-600 rounded-lg bg-purple-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="last"></label> -->
 
  <div class="buttons">
    <button class="border-2 border-pink-500 hover:border-purple-500 ..." @click="create">Create</button>
    <button class="border-2 border-pink-500 hover:border-blue-500 ..." @click="update">Update</button>
    <button class="border-2 border-pink-500 hover:border-yellow-500 ..." @click="del">Delete</button>
  </div>
</div></center>
</template>

<style>
* {
  font-size: inherit;
}
.run{
  height: 450px;
  width: 500px;
  border: solid grey;
}

input {
  display: block;
  margin-bottom: 10px;
}

select {
  float: left;
  margin: 0 1em 1em 0;
  width: 14em;
}

.buttons {
  clear: both;
}

button + button {
  margin-left: 5px;
}
</style>

