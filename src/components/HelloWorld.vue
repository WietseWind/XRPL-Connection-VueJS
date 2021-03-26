<template>
  <div class="hello">
    <h1>XRPL Connection in Vue</h1>
    <button @click="connect('mainnet')">Connect to Mainnet</button>
    <button @click="connect('testnet')">Connect to Testnet</button>
    <h3>{{ net }}</h3>

    <ObjectBrowser :object="msg" />

    <pre>{{ msg }}</pre>
  </div>
</template>

<script>
import Client from 'rippled-ws-client'
import ObjectBrowser from './ObjectBrowser'

export default {
  name: 'HelloWorld',
  components: {
    ObjectBrowser
  },
  data () {
    return {
      net: 'Not connected...',
      msg: {
        some: {
          test: {
            message: true
          }
        }
      },
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
      console.log(typeof this.msg)
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
