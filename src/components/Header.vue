<template>
  <header>
<label> Name:
    <input type="text" name="name" id="name"
    v-model.text:="filter.name"
    step="100"
    >
    </label>
    
    <label>
      Sort By:
      <select v-model="sort.field">
        <option value="name">Name</option>
        <option value="type">Type</option>
        <option value="weight">Weight</option>
      </select>
      <select v-model="sort.direction">
        <option value="1">Ascending order</option>
        <option value="-1">Descending order</option>
      </select>
    </label>
  </header>
</template>

<script>
export default {
  props: {
    filter: Object,
    sort: Object
  }
};
</script>

<style scoped>
header {
  background: steelblue;
  color: white;
  padding: 10px;
}
</style>