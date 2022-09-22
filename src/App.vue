<script setup>
import {ref,computed} from "vue"
const header = ref("Shopping List App")
const items = ref([
  {id:1,label:"10 party hats",purchased: true,highPriority:false},
  {id:1,label:"2 board games",purchased: true,highPriority:false},
  {id:1,label:"20 cups",purchased: false,highPriority:true}
])

const newItem = ref("")
const editing = ref(false)
const characterCount = computed(() => {
  return newItem.value.length
})
const newItemHighPriority = ref(false)
const saveItem = () => {
  items.value.push({id: items.value.length+1,label: newItem.value,highPriority: newItemHighPriority.value})
  newItem.value = ""
  newItemHighPriority.value = ""
}
const doEdit = (e) => {
    editing.value = e
    newItem.value = ""
}
const togglePurchased= (item) => {
  item.purchased = !item.purchased
}
const reversedItems = computed(() => {
  return [...items.value].reverse()
})

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

  <button class="btn btn-primary" @click="saveItem" v-bind:disabled="newItem.length === 0">
    Save Item
  </button>
  </div>
  <p class="counter" v-if="editing">
    {{characterCount}}/200
  </p>

  <ul >
    <li @click="togglePurchased(item)"  v-for="(item) in reversedItems" :key="item.id"  class="static-class" :class="{strikeout: item.purchased, priority:item.highPriority}">{{item.label}}</li>
  </ul>
  <p v-if="!items.length" >
    Nothing to see here
  </p>

</template>