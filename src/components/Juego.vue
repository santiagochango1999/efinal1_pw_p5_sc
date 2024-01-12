<template>
  <div>
    <img :src="url" alt="no funciona" />
    <p>{{ nom }}</p>
  </div>
</template>

<script>
export default {
  props: {
    url: String,
    nom: String,
  },
};
</script>

<style>
img {
  height: 300px;
  width: 300px;
}
</style>