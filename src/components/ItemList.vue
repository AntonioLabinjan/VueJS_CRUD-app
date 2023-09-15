<template>
  <div>
    <h2>Popis stavki:</h2>
    <ul>
      <li v-for="stavka in stavke" :key="stavka.id">
        <div v-if="stavka.id !== (stavkaZaUrediti ? stavkaZaUrediti.id : null)">
          {{ stavka.naziv }}
          <button @click="obrisiStavku(stavka)">Obriši</button>
          <button @click="pripremiUredivanje(stavka)">Uredi</button>
        </div>
        <div v-else>
          <input v-model="stavkaZaUrediti.naziv" @keyup.enter="spasiUredivanje()" />
          <button @click="spasiUredivanje()">Spremi</button>
          <button @click="ponistiUredivanje()">Odustani</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    stavke: Array,
  },
  data() {
    return {
      stavkaZaUrediti: null,
    };
  },
  methods: {
    obrisiStavku(stavka) {
      this.$emit('obrisi-stavku', stavka);
    },
    pripremiUredivanje(stavka) {
      this.stavkaZaUrediti = { ...stavka };
    },
    spasiUredivanje() {
      if (this.stavkaZaUrediti.naziv.trim() !== '') {
        this.$emit('azuriraj-stavku', this.stavkaZaUrediti);
        this.stavkaZaUrediti = null;
      }
    },
    ponistiUredivanje() {
      this.stavkaZaUrediti = null;
    },
  },
};
</script>
