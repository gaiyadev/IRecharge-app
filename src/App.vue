<template>
  <div id="app">
    <div>
      <appbar></appbar>
    </div>
    <router-view />
  </div>
</template>
<script>
import Navbar from "../src/components/Navbar";

export default {
  components: {
    appbar: Navbar
  }
};
</script>

