<template>
    <div class="option">
        <slot/>
    </div>
</template>

<script>
  export default {
    name: 'OptionMcOptionFace.vue'
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
