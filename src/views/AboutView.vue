<template>
  <div id="app">
    <h1 class="nama-pemilik">HI MY WAHYU DWI CANDRA</h1>
    <form @submit.prevent="addItem">
      <input v-model="newItem" placeholder="Tambahkan Kegiatan">
      <button type="submit">ADD</button>
    </form>
    <label>
      <input type="checkbox" v-model="hideCompleted">
      Archive the finished
    </label>
    <ul>
      <li v-for="item in filteredItems" :key="item.id">
        <span :class="{ completed: item.completed }">{{ item.text }}</span>
        <button @click="completeItem(item.id)">Done</button>
        <button @click="deleteItem(item.id)">Delete</button>
      </li>
    </ul>
    <button @click="clearCompleted" class="hapus">Delete the finished learning</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [],
      newItem: '',
      hideCompleted: false,
      idCounter: 0,
    };
  },
  computed: {
    filteredItems() {
      if (this.hideCompleted) {
        return this.items.filter(item => !item.completed);
      }
      return this.items;
    },
  },
  methods: {
    addItem() {
      const newItemText = this.newItem.trim();

      if (newItemText) {
        this.items.push({
          id: this.idCounter++,
          text: newItemText,
          completed: false,
        });

        this.newItem = '';
      }
    },
    completeItem(itemId) {
      const itemIndex = this.items.findIndex(item => item.id === itemId);
      this.items[itemIndex].completed = true;
    },
    deleteItem(itemId) {
      this.items = this.items.filter(item => item.id !== itemId);
    },
    clearCompleted() {
      this.items = this.items.filter(item => !item.completed);
    },
  },
};
</script>
<style>
</style>
