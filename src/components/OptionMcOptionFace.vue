<template>
    <div class="option">
        <h2 :style="`color: ${colour}`">{{ text }}</h2>
    </div>
</template>

<script>
  export default {
    name: 'OptionMcOptionFace.vue',
    props: {
      text: String,
      colour: String,
    }
  }
</script>

<style scoped>
    .option {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
</style>
