<template>
  <div class="hello">
    <h1>XRPL Connection in Vue</h1>
    <button @click="connect('mainnet')">Connect to Mainnet</button>
    <button @click="connect('testnet')">Connect to Testnet</button>
    <h3>{{ net }}</h3>
    <pre>{{ msg }}</pre>
  </div>
</template>

<script>
import Client from 'rippled-ws-client'

export default {
  name: 'HelloWorld',
  data () {
    return {
      net: 'Not connected...',
      msg: '',
      client: null
    }
  },
  methods: {
    connect (net) {
      if (net === 'mainnet') {
        this.net = 'mainnet'
        this.server = 'wss://xrpl.ws'
      } else {
        this.net = 'testnet'
        this.server = 'wss://testnet.xrpl-labs.com'
      }
    }
  },
  watch: {
    async net () {
      this.client = await new Client(this.server, {
        NoUserAgent: true
      })
      this.msg = await this.client.send({ command: 'server_info' })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
