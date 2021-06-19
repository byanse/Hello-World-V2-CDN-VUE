<template>
  <h2>TIPO DE CUENTA {{ cuenta }}</h2>
  <h2>Saldo: {{ saldo }}</h2>
  <h2>Cuenta: {{ estado ? 'Activa' : 'Desactivada' }}</h2>
  <div v-for="(servicio, index) in servicios" :key="index">
    {{ index + 1 }} {{ servicio }}
  </div>
  <AccionSaldo @accion="aumentar" texto="Aumentar Saldo" />
  <!-- Esto "texto" es una props @accion es un custom evento-->
  <AccionSaldo
    texto="Disminuir Saldo"
    @accion="disminuir"
    :desactivar="desactivar"
  />
</template>

<script>
import AccionSaldo from './AccionSaldo.vue';
export default {
  components: {
    AccionSaldo,
  },
  data() {
    return {
      saldo: 1000,
      cuenta: 'Visa',
      estado: true,
      servicios: ['pagos', 'giros', 'transferencias'],
      desactivar: false,
    };
  },
  methods: {
    aumentar() {
      this.saldo = this.saldo + 100;
      this.desactivar = false;
    },
    disminuir() {
      if (this.saldo === 0) {
        this.desactivar = true;
        alert('Saldo Agotado');
        return;
      }
      this.saldo = this.saldo - 100;
    },
  },
};
</script>

<style></style>
