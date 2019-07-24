<template>
    <div id="game">
        <ProgressMcProgressFace/>
        <div id="grid">
            <OptionMcOptionFace/>
            <OptionMcOptionFace>TOP</OptionMcOptionFace>
            <OptionMcOptionFace/>
            <OptionMcOptionFace>LEFT</OptionMcOptionFace>
            <CubyMcCubeFace :rotateTo="rotateTo" @complete="resetRotation"/>
            <OptionMcOptionFace>RIGHT</OptionMcOptionFace>
            <OptionMcOptionFace/>
            <OptionMcOptionFace>BOTTOM</OptionMcOptionFace>
            <OptionMcOptionFace/>
        </div>

    </div>
</template>

<script>
  import ProgressMcProgressFace from './components/ProgressMcProgressFace'
  import CubyMcCubeFace from './components/CubyMcCubeFace'
  import OptionMcOptionFace from './components/OptionMcOptionFace'

  export default {
    name: 'app',
    components: { OptionMcOptionFace, CubyMcCubeFace, ProgressMcProgressFace },

    data () {
      return {
        rotateTo: null,
      }
    },

    methods: {
      onKeyUp (event) {
        switch (event.key) {
          case 'ArrowUp':
            return this.rotate('top')
          case 'ArrowLeft':
            return this.rotate('left')
          case 'ArrowDown':
            return this.rotate('bottom')
          case 'ArrowRight':
            return this.rotate('right')
        }
      },
      rotate (direction) {
        this.rotateTo = direction
      },

      resetRotation () {
        this.rotateTo = null
      }
    },

    created () {
      document.addEventListener('keyup', (event) => this.onKeyUp(event))
    },

    destroyed () {
      document.removeEventListener('keyup', this.onKeyUp)
    }
  }
</script>

<style>
    #game {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    #grid {
        display: grid;
        grid-template-columns: repeat(3, 300px);
        grid-template-rows: repeat(3, 300px);
        border: none;
        margin: 0 auto;
    }
</style>
