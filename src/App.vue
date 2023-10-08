<script setup>
import { ref, reactive, onMounted } from "vue";

const monedas = ref([
  { codigo: "USD", texto: "Dolar de Estados Unidos" },
  { codigo: "MXN", texto: "Peso Mexicano" },
  { codigo: "EUR", texto: "Euro" },
  { codigo: "GBP", texto: "Libra Esterlina" },
]);

const criptomonedas = ref([]);
const cotizar = reactive({
  moneda: "",
  criptomoneda: "",
});

onMounted(() => {
  const url =
    "https://min-api.cryptocompare.com/data/price?fsym=BTC&tsyms=USD,JPY,EUR";
  fetch(url)
    .then((respuesta) => respuesta.json())
    .then(({ Data }) => {
      criptomonedas.value = Data;
    });
});
</script>

<template>
  <div class="contenedor">
    <div class="titulo">Cotizador de <span>Criptomonedas</span></div>
    <div class="contenido">
      <form class="formulario">
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
    </div>
  </div>
</template>
