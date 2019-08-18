<template>
  <ion-button color="light" expand="block" 
  @click="$emit('clear-info')" v-if="info">
  Clear
  </ion-button>
</template>

<script>
export default {
    name: 'ClearInfo',
    props: ['info'],
}
</script>