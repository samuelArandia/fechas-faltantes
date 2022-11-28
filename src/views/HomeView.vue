<template>
  <div class="home">
    <FechasFaltantes msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import FechasFaltantes from '@/components/FechasFaltantes.vue'

export default {
  name: 'HomeView',
  components: {
    FechasFaltantes
  }
}
</script>
