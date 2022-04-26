<template>
  <div class="header q-pt-md q-pb-sm bg-white">
    <div class="header-logo text-center">
      <div class="row">
        <div class="col-12">
          <router-link to="/"
            ><img class="header-logo-img" src="/logo/logotrack.png"
          /></router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  name: "Header",
  methods: {},
};
</script>

<style>
.header-logo-img {
  width: 260px;
}
</style>
