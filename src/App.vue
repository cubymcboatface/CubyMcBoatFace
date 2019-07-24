<template>
    <div id="game">
        <div>Progress Thing</div>
        <ProgressMcProgressFace/>
        <CubyMcCubeFace/>
    </div>
</template>

<script>
  import ProgressMcProgressFace from './components/ProgressMcProgressFace'
  import CubyMcCubeFace from './components/CubyMcCubeFace'

  export default {
    name: 'app',
    components: { CubyMcCubeFace, ProgressMcProgressFace }
  }
</script>

<style>
    #game {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
    }
</style>
