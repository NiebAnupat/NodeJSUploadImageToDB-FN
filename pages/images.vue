<template>
  <div>
    <v-btn @click="returnToHome">ย้อนกลับ</v-btn>
    <!-- แสดงรูปภาพ -->
    <v-row>
      <v-col
        cols="3"
        v-for="(img, index) in allImg"
        :key="index"
        class="red ma-5 rounded-xl"
      >
        <v-img :src="convertBlobToURL(img.data)" class="mt-5 mx-auto"></v-img>
      </v-col>
    </v-row>
  </div>
</template>
<script>
import { Buffer } from 'buffer'
export default {
  async fetch() {
    this.allImg = await this.$axios.$get('http://localhost:4000/images')
  },

  data() {
    return {
      allImg: [],
    }
  },

  methods: {
    // blob to object url
    // https://stackoverflow.com/questions/36280818/how-to-convert-blob-to-object-url
    convertBlobToURL(blob) {
      return (
        'data:image/jpeg;base64,' +
        new Buffer(
          new Uint8Array(blob.data).reduce(
            (data, byte) => data + String.fromCharCode(byte),
            ''
          ),
          'binary'
        ).toString('base64')
      )
    },

    returnToHome() {
      this.$router.push('/')
    },
  },
}
</script>
<style lang="scss"></style>
