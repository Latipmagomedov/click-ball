<template>
  <div class="home">
    <start-screen v-if="startScreen" :lost="lost" @play="play" />
    <game-zone v-if="!startScreen" @lost="lostGame" />
  </div>
</template>

<script>
import StartScreen from '@/components/startScreen'
import GameZone from '@/components/gameZone'

export default {
  name: 'Home',
  components: {
    StartScreen,
    GameZone
  },
  data() {
    return {
      startScreen: true,
      lost: false
    }
  },
  methods: {
    play() {
      this.startScreen = false
    },
    lostGame() {
      this.startScreen = true
      this.lost = true
    }
  }
}
</script>

<style scoped lang="scss">
.home {
  height: 100vh;
  overflow: hidden;
}
</style>
