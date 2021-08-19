<template>
  <Home />
</template>

<script>
import {defineAsyncComponent} from "vue"
export default {
  name: 'App',
  components: {
    Home : defineAsyncComponent(() => import("@/pages/Home"))
  }
}
</script>

