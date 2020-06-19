<template>
  <div>
    <apphome></apphome>
  </div>
</template>

<script>
// @ is an alias to /src
import Home from "@/components/Home.vue";

export default {
  name: "Home",
  components: {
    apphome: Home
  }
};
</script>
