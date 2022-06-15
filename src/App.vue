<template>
  <router-view/>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
  user-select: none;
}

body {
  background-color: #ffffff;
  color: #000000;
  font-family: sans-serif;
}

.container {
  width: 100%;
  max-width: 500px;
  padding: 0 16px;
  margin: 0 auto;
}

input, button {
  border-radius: 0;
  box-shadow: none;
  border: none;
  outline: none;
}

button {
  height: 45px;
  font-size: 16px;
}
</style>
