<template>
  <div class="start-screen">
    <div class="start-screen__wrapper container">
      <div class="start-screen__content">
        <h1 class="start-screen__title">ClickBall</h1>
        <p class="start-screen__record" v-if="record > 0">Ваш рекорд: {{record}}</p>
        <div class="start-screen__btns">
          <button class="start-screen__btn start-screen__btn_start" @click="$emit('play')">Начать</button>
          <button class="start-screen__btn start-screen__btn_settings">Настройки</button>
        </div>

        <p class="start-screen__lost" v-if="lost">Вы проиграли</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'StartScreen',
  props: {
    lost: {
      default: false,
      type: Boolean
    }
  },
  data() {
    return {
      record: localStorage.getItem('record') ? localStorage.getItem('record') : 0
    }
  }
}
</script>

<style scoped lang="scss">
.start-screen {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(#CE9FFC, #7367F0);
  color: #fff;

  &__wrapper {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  &__content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  &__title {
    margin-top: -100px;
    font-size: 35px;
  }

  &__record {
    margin-top: 5px;
    font-size: 17px;
    font-weight: 600;
  }

  &__lost {
    margin-top: 15px;
    font-size: 13px;
  }

  &__btns {
    width: 200px;
    margin-top: 20px;
    display: flex;
    flex-direction: column;
  }

  .start-screen__btn {
    border-radius: 10px;

    &:not(:first-child) {
      margin-top: 5px;
    }

    &_start {
      background-color: $blue;
      color: #fff;
    }

    &_settings {
      background-color: #7AB1FF;
      color: #fff;
    }
  }
}
</style>
