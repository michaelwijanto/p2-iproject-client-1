<template>
  <div class="flex items-center justify-center">
      <a href="#" @click.prevent="selectImage(imgUrl)">
      <img :src="imgUrl" alt="Avatar image" width="200px" height="300px"/>
      </a>
  </div>
</template>

<script>
export default {
    name: "ImageCard",
    props:["imgUrl"],
    methods: {
        selectImage(imgUrl) {
            console.log("test", imgUrl)
            this.$emit("selected", imgUrl)
        }
    }
}
</script>

<style>

</style>