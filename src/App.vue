<script setup>
import {ref} from "vue"
const header = ref("Shopping List App")
const items = ref([
])

const newItem = ref("")
const editing = ref(false)
const newItemHighPriority = ref(false)
const saveItem = () => {
  items.value.push({id: items.value.length+1,label: newItem.value})
  newItem.value = ""
}
const doEdit = (e) => {
    editing.value = e
    newItem.value = ""
}


</script>


<template>
<div class="header">
  <h1>{{header}}</h1>
  <button class="btn" v-if="editing" @click="doEdit(false)">Cancel</button>
  <button v-else class="btn btn-primary" @click="doEdit(true)">Add Item</button>
</div>

  <div class="add-item-form" v-if="editing" >
  <input type="text" placeholder="Add an item" v-model.trim="newItem">
  <label>
    <input type="checkbox" v-model="newItemHighPriority">
    High Priority
  </label>
  <br>

  <button class="btn btn-primary" @click="saveItem">
    Save Item
  </button>
  </div>

  <ul v-if="editing">
    <li  v-for="({id,label}) in items" :key="id">{{label}}</li>
  </ul>
  <p v-if="!items.length" >
    Nothing to see here
  </p>

</template>