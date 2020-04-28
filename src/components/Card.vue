<template>
  <div class="card">
    <div class="card-content" @click="modalOpen = true">
      <img class="card-photo" :src="photo.media.m">
    </div>
    <app-modal v-if="modalOpen" @close="modalOpen = false" :photo="photo"></app-modal>
  </div>
</template>

<script>
import $ from 'jquery'
import appModal from './Modal'

export default {
  name: 'card',
  data () {
    return {
      modalOpen: false
    }
  },
  components: {
    'app-modal': appModal,
  },
  props: ['photo']
}
</script>

<style scoped lang="scss">
    @import "~/assets/scss/modules/_cards.scss"
</style>
