<template>
  <q-page class="q-py-md container">
    <div class="row flex justify-center">
      <div class="col-12 flex flex-center text-white q-px-md q-pb-sm">
        <p class="q-pa-none q-ma-none">
          Rastreie aqui sua encomenda dos Correios, informando o código recebido
          no momento da postagem pelo remetente. A aplicação usa a api
          <a
            href="https://api.linketrack.com/"
            class="text-white"
            target="_blank"
            >LINK&TRACK</a
          >, para obter o rastreamento da encomenda.
        </p>
      </div>
      <div class="col-11 col-md-5">
        <q-input
          dense
          color="white"
          label-color="black"
          borderless
          bg-color="white"
          outlined
          v-model="tracking_code"
          placeholder="Digite aqui o numero de rastreio"
        >
          <template v-slot:after>
            <q-btn
              @click="handleGetPackage"
              class="full-height full-width text-black bg-secondary"
            >
              <i class="text-h6 ri-search-line"></i>
            </q-btn>
          </template>
        </q-input>
      </div>
    </div>

    <div
      class="col-12 flex flex-center text-white q-pa-sm"
      v-if="error_resp && !thepackage.codigo"
    >
      Não foi possivel obter os dados, tente novamente
    </div>

    <div
      class="col-12 flex flex-center text-white q-py-md"
      v-if="thepackage.codigo"
    >
      <div class="col-12">
        <div class="text-h6 q-ma-none">Código: {{ thepackage.codigo }}</div>
        <div class="text-subtitle2">Atualização: {{ thepackage.ultimo }}</div>
        <div class="text-subtitle2">Serviço: {{ thepackage.servico }}</div>
      </div>
    </div>

    <div class="row q-pa-sm" v-if="thepackage.eventos">
      <div
        class="col-12 col-md-6 offset-md-3 q-mb-sm"
        v-for="(evento, ikey) in thepackage.eventos"
        :key="ikey"
      >
        <Item :packpage="evento" />
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref, onMounted, onBeforeMount } from "vue";
import { api } from "boot/axios";
import { useQuasar } from "quasar";
import Item from "components/Packpage/Item.vue";

export default defineComponent({
  name: "Correios",
  components: { Item },
  setup() {
    const tracking_code = ref("");
    const thepackage = ref([]);
    const error_resp = ref(false);
    const $q = useQuasar();

    const handleGetPackage = async () => {
      $q.loading.show();
      try {
        thepackage.value = [];
        await api
          .get(
            "https://api.linketrack.com/track/json?user=teste&token=1abcd00b2731640e886fb41a8a9671ad1434c599dbaa0a0de9a5aa619f29a83f&codigo=" +
              tracking_code.value
          )
          .then((res) => {
            thepackage.value = res.data;
          });
        mesage.value.status = true;
        $q.loading.hide();
      } catch (error) {
        if (error.response && error.response.status == "429") {
          await handleGetPackage();
        } else error_resp.value = true;
        $q.loading.hide();
      }
    };
    return {
      tracking_code,
      thepackage,
      error_resp,
      handleGetPackage,
    };
  },
});
</script>
