<template>
  <div class="container">
    <img :src="urlImg" alt="No se muestra imagen" />
    <h1>{{ texto }}</h1>
  </div>
</template>
  
  <script>
export default {
  props: {
    texto: {
      type: String
    },
    urlImg: {
      type: String
    }
  }
};
</script>
  
<style scoped>
.container {
  display: grid;
  justify-content: center;
  align-items: center;
}

img {
  width: 150px;
  height: 200px;
  padding-left: 430px;
}
h1 {
  font-size: 20px;
  padding-left: 200px;
}
</style>