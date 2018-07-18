<template>
<div class="test">
  <h5>{{ message }}</h5>
  <input v-model="message" />
</div>
</template>

<script>
export default {
  data: () => ({
    message: 'hello world',
  }),
}
</script>
