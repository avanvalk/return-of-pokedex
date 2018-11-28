<template>
  <header>

    <label for="name"> Name:
    <input type="text" name="name" id="name"
    v-model.text:="filter.name"
    >
    </label>

    
    
    <label for="sort">
      Sort By:
      <select v-model="sort.field">
        <option value="name">Name</option>
        <option value="type_1">Type</option>
        <option value="attack">Attack</option>
        <option value="defense">Defense</option>
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
  background: black;
  color: white;
  padding: 5px;
}
</style>