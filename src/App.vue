<template>
    <div id="game">
        <ProgressMcProgressFace/>
        <div id="grid">
            <OptionMcOptionFace/>
            <OptionMcOptionFace text="Top" colour="green"/>
            <OptionMcOptionFace/>
            <OptionMcOptionFace text="Left" colour="red"/>
            <CubyMcCubeFace :rotateTo="rotateTo" :frontFace="frontFace" :nextFace="nextFace"
                            @complete="resetRotation"/>
            <OptionMcOptionFace text="Right" colour="blue"/>
            <OptionMcOptionFace/>
            <OptionMcOptionFace text="Bottom" colour="orange"/>
            <OptionMcOptionFace/>
        </div>

    </div>
</template>

<script>
  import ProgressMcProgressFace from './components/ProgressMcProgressFace'
  import CubyMcCubeFace from './components/CubyMcCubeFace'
  import OptionMcOptionFace from './components/OptionMcOptionFace'

  const randomOption = () => ''

  export default {
    name: 'app',
    components: { OptionMcOptionFace, CubyMcCubeFace, ProgressMcProgressFace },

    data () {
      return {
        rotateTo: null,
        frontFace: randomOption(),
        options: {
          top: randomOption(),
          left: randomOption(),
          right: randomOption(),
          bottom: randomOption(),
        },
        nextFace: '',
      }
    },

    methods: {
      randomizeOptions () {
        this.options.top = randomOption()
        this.options.left = randomOption()
        this.options.bottom = randomOption()
        this.options.right = randomOption()
      },

      onKeyUp (event) {
        if (this.rotateTo) {
          return
        }

        switch (event.key) {
          case 'ArrowUp':
            return this.rotate('bottom')
          case 'ArrowLeft':
            return this.rotate('right')
          case 'ArrowDown':
            return this.rotate('top')
          case 'ArrowRight':
            return this.rotate('left')
        }
      },

      rotate (direction) {
        this.rotateTo = direction
      },

      resetRotation () {
        this.rotateTo = null
        const tempFace = this.frontFace
        this.frontFace = this.nextFace
        this.nextFace = tempFace
        this.randomizeOptions()
      }
    },

    created () {
      document.addEventListener('keyup', (event) => this.onKeyUp(event))
      this.randomizeOptions()
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
