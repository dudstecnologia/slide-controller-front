<template>
  <div class="row q-col-gutter-sm">
    <div class="col-12">
      <q-btn class="full-width" color="black" label="Iniciar Apresentação" @click="sendCommand('f5')" />
    </div>
    <div class="col-6">
      <q-btn class="full-width" color="black" icon="navigate_before" size="lg" style="height: 150px" @click="sendCommand('left')" />
    </div>
    <div class="col-6">
      <q-btn class="full-width" color="black" icon="navigate_next" size="lg" style="height: 150px" @click="sendCommand('right')" />
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ReaderCode',

  props: {
    uuid: {
      type: String,
      required: true
    }
  },

  data () {
    return {
      client: null,
      connected: false
    }
  },

  mounted () {
    this.initConnect()
  },

  methods: {
    initConnect () {
      // http
      // wss://broker.emqx.io:8083/mqtt
      // https
      // wss://broker.emqx.io:8084/mqtt
      this.client = mqtt.connect('wss://broker.emqx.io:8084/mqtt', {
        clean: true,
        connectTimeout: 4000,
        clientId: `scm-${this.uuid.substring(0, 7)}`
      })

      this.client.on('connect', () => {
        this.connected = true
      })
    },

    sendCommand (command) {
      if (this.connected) {
        this.client.publish(`slider-controller/${this.uuid}`, command)
      }
    }
  }
})
</script>
