<template>
  <q-page class="q-pa-md q-gutter-y-sm">
    <q-input v-if="debug" v-model="uuid" label="UUID" />

    <reader-code v-if="!showController" @set-uuid="setUuid" />
    <slide-controller v-else :uuid="uuid" />
  </q-page>
</template>

<script>
import ReaderCode from 'src/components/ReaderCode.vue';
import SlideController from 'src/components/SlideController.vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'IndexPage',

  components: {
    ReaderCode,
    SlideController
  },

  data () {
    return {
      uuid: '',
      debug: false,
      showController: false
    }
  },

  methods: {
    setUuid (uuid) {
      if (this.checkValidUUID(uuid)) {
        this.uuid = uuid
        this.showController = true
      }
    },

    checkValidUUID (str) {
      const regexExp = /^[0-9a-fA-F]{8}\b-[0-9a-fA-F]{4}\b-[0-9a-fA-F]{4}\b-[0-9a-fA-F]{4}\b-[0-9a-fA-F]{12}$/gi
      return regexExp.test(str)
    }
  }

});
</script>
