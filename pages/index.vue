<template>
  <div>
    <h1>อัปโหลดรูปภาพ</h1>
    <v-btn @click="nextPage">ดูรูปภาพทั้งหมด</v-btn>
    <v-file-input
      label="File input"
      accept="image/png, image/jpeg, image/bmp"
      prepend-icon="mdi-camera"
      @change="Preview_image"
      v-model="image"
      name="image"
    ></v-file-input>
    <v-btn block color="primary" @click="uploadImage">อัปโหลด</v-btn>
    <div class="red">
      <v-img :src="url" class="mt-5 mx-auto"></v-img>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      url: null,
      image: null,
    }
  },
  methods: {
    Preview_image() {
      this.url = URL.createObjectURL(this.image)
    },

    uploadImage() {
      const formData = new FormData()
      formData.append('image', this.image)
      console.log('>> formData >> ', formData)
      this.$axios
        .post('http://localhost:4000/upload', formData, {
          headers: {
            'Content-Type': 'multipart/form-data',
          },
        })
        .then((res) => {
          console.log(res)
        })
        .catch((err) => {
          console.log(err)
        })
    },

    nextPage() {
      this.$router.push('/images')
    },
  },
}
</script>
<style lang="scss"></style>
