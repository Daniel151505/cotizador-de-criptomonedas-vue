<script setup>
import { ref } from "vue";

const monedas = ref([
  { codigo: "USD", texto: "Dolar de Estados Unidos" },
  { codigo: "MXN", texto: "Peso Mexicano" },
  { codigo: "EUR", texto: "Euro" },
  { codigo: "GBP", texto: "Libra Esterlina" },
]);
</script>

<template>
  <div class="contenedor">
    <div class="titulo">Cotizador de <span>Criptomonedas</span></div>
    <div class="contenido">
      <div class="formulario">
        <div class="campo">
          <label for="moneda">Moneda:</label>
          <select id="moneda">
            <option value="">-- Selecciona --</option>
            <option v-for="moneda in monedas" :value="moneda.codigo">
              {{ moneda.texto }}
            </option>
          </select>
        </div>
      </div>
    </div>
  </div>
</template>
