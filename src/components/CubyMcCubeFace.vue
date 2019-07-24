<template>
    <div class="scene">
        <div :class="getClassForCube()" @transitionend="transitionComplete">
            <div class="cube__face cube__face--front">front</div>
            <div class="cube__face cube__face--right">right</div>
            <div class="cube__face cube__face--left">left</div>
            <div class="cube__face cube__face--top">top</div>
            <div class="cube__face cube__face--bottom">bottom</div>
        </div>
    </div>
</template>

<script>
  export default {
    name: 'CubyMcCubeFace',

    props: {
      rotateTo: String,
    },

    methods: {
      transitionComplete () {
        this.$emit('complete')
      },

      getClassForCube () {
        return this.rotateTo
          ? `cube with-transition show-${this.rotateTo}`
          : 'cube'
      }
    }
  }
</script>


<style scoped lang="scss">
    $size: 300px;

    .scene {
        width: $size;
        height: $size;
        perspective: 400px;
        margin: 0 auto;
    }

    .cube {
        width: 100%;
        height: 100%;
        position: relative;
        transform-style: preserve-3d;
        transform: translateZ(calc(#{$size} / -2));


        &.with-transition {
            transition: transform .3s ease-in-out;
        }
    }

    .cube__face {
        position: absolute;
        width: $size;
        height: $size;
        border: 1px solid #000;
        text-align: center;
        font-size: 3rem;
        background-color: rgba(255, 255, 255, 0.6);
    }

    .cube__face--front {
        transform: rotateY(0deg) translateZ(calc(#{$size} / 2));

    }

    .cube__face--right {
        transform: rotateY(90deg) translateZ(calc(#{$size} / 2));

    }

    .cube__face--left {
        transform: rotateY(-90deg) translateZ(calc(#{$size} / 2));

    }

    .cube__face--top {
        transform: rotateX(90deg) translateZ(calc(#{$size} / 2));

    }

    .cube__face--bottom {
        transform: rotateX(-90deg) translateZ(calc(#{$size} / 2));

    }

    .cube.show-front {
        transform: translateZ(calc(#{$size} / -2)) rotateY(0deg);

    }

    .cube.show-right {
        transform: translateZ(calc(#{$size} / -2)) rotateY(-90deg);

    }

    .cube.show-left {
        transform: translateZ(calc(#{$size} / -2)) rotateY(90deg);

    }

    .cube.show-top {
        transform: translateZ(calc(#{$size} / -2)) rotateX(-90deg);

    }

    .cube.show-bottom {
        transform: translateZ(calc(#{$size} / -2)) rotateX(90deg);

    }
</style>
