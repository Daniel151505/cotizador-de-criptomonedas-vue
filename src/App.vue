<script setup>
import { ref, reactive } from "vue";
import AlertaVue from "./components/Alerta.vue";
import SpinnerVue from "./components/Spinner.vue";
import CotizacionVue from "./components/Cotizacion.vue";
import useCripto from "./composables/useCripto";

const {
  monedas,
  criptomonedas,
  cargando,
  cotizacion,
  obtenerCotizacion,
  mostrarResultado,
} = useCripto();
const error = ref("");
const cotizar = reactive({
  moneda: "",
  criptomoneda: "",
});

const cotizarCripto = () => {
  // Validar que cotizar este lleno
  if (Object.values(cotizar).includes("")) {
    error.value = "Todos los campos son obligatorios";

    setTimeout(() => {
      error.value = "";
    }, 2000);
    return;
  }

  obtenerCotizacion(cotizar);
};
</script>

<template>
  <div class="contenedor">
    <div class="titulo">Cotizador de <span>Criptomonedas</span></div>
    <div class="contenido">
      <AlertaVue v-if="error"> {{ error }}</AlertaVue>
      <form class="formulario" @submit.prevent="cotizarCripto">
        <div class="campo">
          <label for="moneda">Moneda:</label>
          <select id="moneda" v-model="cotizar.moneda">
            <option value="">-- Selecciona --</option>
            <option v-for="moneda in monedas" :value="moneda.codigo">
              {{ moneda.texto }}
            </option>
          </select>
        </div>

        <div class="campo">
          <label for="cripto">Criptomoneda:</label>
          <select id="cripto" v-model="cotizar.criptomoneda">
            <option value="">-- Selecciona --</option>
            <option
              v-for="criptomoneda in criptomonedas"
              :value="criptomoneda.CoinInfo.Name"
            >
              {{ criptomoneda.CoinInfo.FullName }}
            </option>
          </select>
        </div>

        <input type="submit" value="Cotizar" />
      </form>

      <SpinnerVue v-if="cargando" />

      <CotizacionVue v-if="mostrarResultado" :cotizacion="cotizacion" />
    </div>
  </div>
</template>
