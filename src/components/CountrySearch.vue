<template>
  <main class="container">
    <div>
      <input class="search-bar" type="text" placeholder="Search..." :value="modelValue" @input="$emit('update:modelValue', $event.target.value)">
    </div>
  </main>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: String,
      require: true
    }
  }
}
</script>

<style scoped>


.search-bar:focus {
  box-shadow: 0 0 16px;
  background-color: white;
}

.search-bar {
  display: block;
  width: 100%;
  padding: 16px;
  margin-top: 20px;

  color: #313131;
  font-size: 20px;
  border: none;
  appearance: none;
  outline: none;
  background-color: rgba(132, 186, 217, 0.75);
  border-radius: 16px;
  transition: 0.4s;
  box-shadow: 3px 3px rgba(0, 0, 0, 0.25);
}
</style>