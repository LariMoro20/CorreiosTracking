<template>
  <footer>
    <div class="row">
      <div class="tracking__footer col-12 q-py-sm text-center flec column">
        <router-link to="/"
          ><img class="footer__logo-img" src="/logo/logotrack.png"
        /></router-link>
        <small>{{ year }} &copy; Lari Moro</small>
      </div>
    </div>
  </footer>
</template>
<script>
export default {
  name: "Footer",
  data: () => ({
    year: new Date().getFullYear(),
  }),
};
</script>
<style scoped>
.tracking__footer {
  background-color: white;
  color: black;
}
a {
  text-decoration: none;
}
.footer__logo-img {
  width: 70px;
}
</style>
