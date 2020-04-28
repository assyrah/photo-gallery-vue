<template>
    <transition name="modal-fade">
        <div id="app-modal">
            <div class="modal-layer">
                <div class="modal">
                    <header class="modal-header">
                        <button
                            type="button"
                            class="button button--text button--lg close"
                            @click="close"
                        >
                            X
                        </button>
                    </header>
                    <section class="modal-body row">
                        <div class="modal-left">
                            <img class="photo" @click.stop :src="getPhotoUrl()">
                        </div>
                        <div class="modal-right">
                            <h3>Image Details</h3>
                            <small class="modal-description" v-if="getDescription()">{{ getDescription() }}</small>
                            <small class="modal-description" v-else>No description to show.</small>
                        </div>
                    </section>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
import $ from 'jquery'
export default {
  name: 'modal',
  props: ['photo'],
  methods: {
    close: function() {
        this.$emit('close');
    },
    getPhotoUrl: function () {
      const original = this.photo.media.m
      console.log(this.photo.media.m.substring(0, original.length - 5))
      return this.photo.media.m.substring(0, original.length - 5) + 'b.jpg'
    },
    getDescription: function () {
      // extract the actual text since the the actual text is in HTML
      var span = document.createElement('span')
      span.innerHTML = this.photo.description
      const contents = span.textContent || span.innerText
      // omit the 'username posted a photo:' texts
      return $.trim(contents.split('posted a photo:')[1])
    }
  }
}
</script>

<style scoped lang="scss">
    @import "~/assets/scss/modules/_modal.scss"
</style>
