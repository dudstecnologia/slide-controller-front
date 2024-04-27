<template>
  <qrcode-stream @detect="onDetect" :formats="['qr_code']"></qrcode-stream>
</template>

<script>
import { QrcodeStream } from 'vue-qrcode-reader'
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ReaderCode',

  components: {
    QrcodeStream
  },

  methods: {
    onDetect (detectedCodes) {
      if (detectedCodes[0] && detectedCodes[0].rawValue) {
        this.$emit('setUuid', detectedCodes[0].rawValue)
      }
    }
  }
})
</script>
