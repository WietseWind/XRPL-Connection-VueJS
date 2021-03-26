<template>
  <div class="object-container">
    <div v-if="typeof object === 'object' && object !== null">
      <ul>
        <li v-for="key in Object.keys(object)" v-bind:key="key">
          <code>{{ key }}</code> ({{ typeof key }}):
          <ObjectBrowser :object="object[key]" />
        </li>
      </ul>
    </div>
    <div v-else>
      {{ typeof object }}: <pre>{{ object }}</pre>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ObjectBrowser',
  props: ['object']
}
</script>

<style scoped lang="scss">
  div.object-container {
    padding: 10px; margin: 10px; border: 1px solid red;

    code {
      border: 1px solid #666; background-color: grey;
      padding: 2px 10px; color: white;
    }
  }
</style>
