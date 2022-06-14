<template>
  <div class="game">
    <div class="game__header">
      <div class="game__header-wrapper container">
        <div class="game__header-exit">Закончить</div>
        <div class="game__header-nums">
          <span>Счет - {{ points }}</span>
          <span>Промохов - {{ numberMisses }}</span>
        </div>
      </div>
    </div>
    <div class="game__zone container" ref="gameZone" @click.self="missed">
      <div class="game__ball"
           v-for="(ball, index) in balls"
           :key="index"
           @click="deleteBall(index)"
           :class="{'game__ball_delete': ball.animation}"
           :style="{
             left: `${ball.x}px`,
             top: `${ball.y}px`,
             width: this.properties.w,
             height: this.properties.h,
           }">
        <span :style="{backgroundColor: ball.bg}"></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GameZone',
  data() {
    return {
      properties: {
        w: '50px',
        h: '50px',
        interval: 500,
        lost: 10,
        maxBall: 20
      },
      audio: {
        explosion: require('@/assets/audio/explosion.mp3')
      },
      colors: ['#5199FF', '#FFBEED', '#FBCEB5', '#FED876'],
      balls: [],
      oldRecord: localStorage.getItem('record') ? localStorage.getItem('record') : 0,
      points: 0,
      numberMisses: 0
    }
  },
  mounted() {
    this.createBall()
  },
  methods: {
    getRandomArbitrary(min, max) {
      return Math.round(Math.random() * (max - min) + min);
    },
    createBall() {
      setInterval(() => {
        if (!this.$refs.gameZone) return
        const w = this.$refs.gameZone.offsetWidth
        const h = this.$refs.gameZone.offsetHeight

        this.balls.push({
          x: this.getRandomArbitrary(0, w),
          y: this.getRandomArbitrary(0, h),
          bg: this.colors[this.getRandomArbitrary(0, this.colors.length - 1)],
          animation: false
        })

        if (this.balls.length === this.properties.maxBall) this.$emit('lost')
      }, this.properties.interval)
    },
    deleteBall(index) {
      this.balls[index].animation = true
      setTimeout(() => this.balls.splice(index, 1), 100)
      this.points++
      new Audio(this.audio.explosion).play()

      if (this.points > this.oldRecord) localStorage.setItem('record', this.points)
    },
    missed() {
      this.numberMisses++
      if (this.numberMisses === this.properties.lost) this.$emit('lost')
    }
  }
}
</script>

<style scoped lang="scss">
.game {
  width: 100%;
  height: 100vh;
  background: linear-gradient(#CE9FFC, #7367F0);

  &__header {
    width: 100%;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: rgba(66, 83, 89, 0.34);
  }

  &__header-wrapper {
    display: flex;
    justify-content: space-between;
  }

  &__header-exit {
    color: #fff;
    font-size: 16px;
    font-weight: 600;
  }

  &__header-nums {
    span {
      font-size: 14px;

      &:not(:first-child) {
        margin-left: 10px;
      }
    }
  }

  &__zone {
    position: relative;
    height: calc(100vh - 50px);
    overflow: hidden;
  }

  &__ball {
    position: absolute;
    border-radius: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: width .2s, height .2s;
    cursor: pointer;

    span {
      display: block;
      width: 100%;
      height: 100%;
      border-radius: 100%;
      border: .2px solid #ffffff;
      transition: width .2s, height .2s;
    }

    &_delete {
      span {
        width: 0;
        height: 0;
      }
    }
  }
}
</style>
