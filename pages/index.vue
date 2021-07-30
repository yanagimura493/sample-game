<template>
  <div class="place" ref="place">
    <div
      class="hero"
      ref="hero"
      :style="`transform: translate(${coordX}px, ${coordY}px)`"
    >
      <img
        src="~/assets/hero.gif"
        class="hero"
      />
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    coordY: 0,
    coordX: 0,
    place: null,
    hero: null,
  }),
  mounted() {
    const code = {
      top: 38,    // 上
      bottom: 40, // 下
      left: 37,   // 左
      right: 39,  // 右
    }

    const heroWidth = this.$refs.hero.clientWidth
    const heroHeight = this.$refs.hero.clientHeight

    const maxX = this.$refs.place.clientWidth - heroWidth
    const maxY = this.$refs.place.clientHeight - heroHeight

    window.onkeydown = (e) => {
      const keyCode = e.keyCode

      const move = 12

      if (keyCode === code.top) {
        this.coordY = this.coordY > 0 ? this.coordY - move : this.coordY
      }

      if (keyCode === code.bottom) {
        let coordY = this.coordY + move

        if (coordY > maxY) {
          coordY = maxY
        }

        this.coordY = coordY
      }

      if (keyCode === code.left) {
        this.coordX = this.coordX > 0 ? this.coordX - move : this.coordX
      }

      if (keyCode === code.right) {
        let coordX = this.coordX + move

        if (coordX > maxX) {
          coordX = maxX
        }

        this.coordX = coordX
      }
    }
  }
}
</script>

<style>
.place {
  position: relative;
  width: 400px;
  height: 400px;
  background-image: url('~/assets/leaf.png');
}

.hero {
  display: block;
  position: relative;
  width: 160px;
}

.hero img {
  width: 100%;
  transform: rotateY(180deg);
}
</style>
