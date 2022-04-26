<template>
  <div class="flex packpage__item q-pa-sm">
    <div class="flex">
      <q-avatar size="80px">
        <img src="/images/caminhao.png" />
      </q-avatar>
      <div class="text-white flex items-center">
        <p class="q-pa-none q-ma-none">
          {{ packpage.status }}<br />
          Data: {{ packpage.data }} {{ packpage.hora }}<br />
          <span v-if="status.length" style="font-size: 12px"
            >{{ status[0] }} <br />Para:{{ status[1] }}</span
          >
          <span v-else> {{ packpage.local }}</span>
        </p>
      </div>
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
  data: () => ({
    status: [],
  }),

  mounted() {
    if (this.packpage.subStatus[0]) {
      this.status = this.packpage.subStatus[0].split("Para:");
    }
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
