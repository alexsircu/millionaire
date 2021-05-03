<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <Container/>
  </div>
</template>

<script>
// @ is an alias to /src
import Container from "@/components/Container.vue";

export default {
  name: "Home",
  components: {
    Container
  }
};
</script>
