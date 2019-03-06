<template>
  <table>
    <li>
      {{ todo.text }} from {{ todo.author ? todo.author : "Anonymous" }}
      <button @click="$emit('remove', todo.id);">X</button>
    </li>
    <slot name="first"> </slot>
    <slot slot="last"> </slot>
  </table>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  }
};
</script>
