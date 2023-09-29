<template>
  <div class="bg-gray-900 text-white min-h-screen">
    <Nav />
    <div class="container mx-auto mt-24 md:mt-16">
      <router-view :key="$route.path" />
    </div>
    <!-- set progressbar -->
    <vue-progress-bar></vue-progress-bar>
    <Footer></Footer>
  </div>
</template>

<script>
import Nav from "./components/TheNavigation";
import Footer from "./components/TheFooter";

export default {
  components: {
    Nav,
    Footer
  },
  created() {
    
    this.$Progress.start();
    this.$router.beforeEach((to, from, next) => {
      if (to.meta.progress !== undefined) {
        let meta = to.meta.progress;
        this.$Progress.parseMeta(meta);
      }
     
      this.$Progress.start();
      next();
    });
    
    this.$store.dispatch("genre/getGenre");

    this.$router.afterEach(() => {
      this.$Progress.finish();
    });
  },
  mounted() {
    this.$Progress.finish();
  }
};
</script>
<style>
</style>
