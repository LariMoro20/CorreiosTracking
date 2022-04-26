<template>
  <div class="flex packpage__item q-pa-sm">
    <q-avatar size="80px">
      <img src="/images/caminhao.png" />
    </q-avatar>
    <div class="col-8 text-white flex items-center">
      <p class="q-pa-none q-ma-none">
        {{ packpage.status }}<br />
        Data: {{ packpage.data }} {{ packpage.hora }}<br />
        {{ packpage.local }}<br />
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    packpage: {
      type: [Array, Object],
      default: null,
    },
  },
};
</script>

<style scoped>
.packpage__item {
  border-left: 3px dashed #bcbcbc;
}
.packpage__item::before {
  content: "---";
  color: #bcbcbc;
  display: flex;
  align-content: center;
  justify-content: center;
  align-items: center;
  font-size: 2.2rem;
}
</style>
