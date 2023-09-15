<template>
  <div>
    <h2>Unesite novu stavku:</h2>
    <input v-model="novaStavka" @keyup.enter="dodajStavku" />
    <button @click="dodajStavku">Dodaj</button>
    <!-- Dodaj gumb za ažuriranje samo ako je u tijeku uređivanje -->
    <button v-if="jeUreduStavka" @click="azurirajStavku">Ažuriraj</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      novaStavka: '',
      jeUreduStavka: false, // Dodaj varijablu za praćenje uređivanja
    };
  },
  methods: {
    dodajStavku() {
      if (this.novaStavka.trim() !== '') {
        this.$emit('dodaj-stavku', this.novaStavka);
        this.novaStavka = '';
      }
    },
    azurirajStavku() {
      if (this.novaStavka.trim() !== '') {
        this.$emit('azuriraj-stavku', this.novaStavka);
        this.novaStavka = '';
        this.jeUreduStavka = false; // Završi uređivanje nakon ažuriranja
      }
    },
  },
};
</script>
