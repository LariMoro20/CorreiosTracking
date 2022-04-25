<template>
  <q-layout view="lHh Lpr lFf" class="bg-primary">
    <Header />
    <q-page-container class="countries__pages">
      <router-view class="countrie__page" />
    </q-page-container>
    <Footer />
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import Header from "components/Parts/Header.vue";
import Footer from "components/Parts/Footer.vue";
export default defineComponent({
  name: "MainLayout",

  components: {
    Header,
    Footer,
  },

  setup() {
    return {};
  },
});
</script>
<style>
* {
  font-family: "Josefin Sans", sans-serif;
}
</style>
