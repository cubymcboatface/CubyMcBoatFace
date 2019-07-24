<template>
    <div id="game">
        <ProgressMcProgressFace/>
        <div id="grid">
            <OptionMcOptionFace/>
            <OptionMcOptionFace><img class="option" :src="options.top"/></OptionMcOptionFace>
            <OptionMcOptionFace/>
            <OptionMcOptionFace><img class="option" :src="options.left"/></OptionMcOptionFace>
            <CubyMcCubeFace :rotateTo="rotateTo" :frontFace="frontFace" :nextFace="nextFace" @complete="resetRotation"/>
            <OptionMcOptionFace><img class="option" :src="options.right"/></OptionMcOptionFace>
            <OptionMcOptionFace/>
            <OptionMcOptionFace><img class="option" :src="options.bottom"/></OptionMcOptionFace>
            <OptionMcOptionFace/>
        </div>

    </div>
</template>

<script>
  import ProgressMcProgressFace from './components/ProgressMcProgressFace'
  import CubyMcCubeFace from './components/CubyMcCubeFace'
  import OptionMcOptionFace from './components/OptionMcOptionFace'
  import boat from './assets/boat.jpeg'
  import jeremy from './assets/jeremy.jpg'
  import flange from './assets/flange.png'
  import skrunky from './assets/skrunky.jpeg'
  import spanners from './assets/spanners.jpeg'

  const allImages = [boat, jeremy, flange, skrunky, spanners]

  const randomImage = () => allImages[Math.floor(Math.random() * allImages.length)]

  export default {
    name: 'app',
    components: { OptionMcOptionFace, CubyMcCubeFace, ProgressMcProgressFace },

    data () {
      return {
        rotateTo: null,
        frontFace: randomImage(),
        options: {
          top: randomImage(),
          left: randomImage(),
          right: randomImage(),
          bottom: randomImage(),
        },
        nextFace: '',
      }
    },

    methods: {
      randomizeOptions () {
        this.options.top = randomImage()
        this.options.left = randomImage()
        this.options.bottom = randomImage()
        this.options.right = randomImage()
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
        this.nextFace = this.options[direction]
        this.options[direction] = this.nextFace

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

    .option {
        width: 100px;
        height: 100px;
    }
</style>
