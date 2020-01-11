<template>
  <div>
    <form @submit="addItem">
      Add new todo item:
      <input type="text" v-model="title">
      <input type="submit" value="Add">
    </form>
  </div>
</template>


<script>
export default {
  name: 'AddItem',
  data() {
    return {
      title: ''
    }
  },
  methods: {
    addItem(e) {
      e.preventDefault();
      const newItem = {
        title: this.title,
        completed: false
      }
      // send up to parent
      this.$emit('add-item', newItem);
      this.title='';
    }
  }
}
</script>


<style  scoped>
</style>