<template>
  <div>
    <ItemList :stavke="stavke" @obrisi-stavku="obrisiStavku" @azuriraj-stavku="azurirajStavku" />
    <ItemForm @dodaj-stavku="dodajStavku" />
  </div>
</template>

<script>
import ItemList from './components/ItemList.vue';
import ItemForm from './components/ItemForm.vue';

export default {
  components: {
    ItemList,
    ItemForm,
  },
  data() {
    return {
      stavke: [],
    };
  },
  methods: {
    dodajStavku(novaStavka) {
      this.stavke.push({ id: this.stavke.length + 1, naziv: novaStavka });
    },
    obrisiStavku(stavkaZaBrisanje) {
      this.stavke = this.stavke.filter(stavka => stavka !== stavkaZaBrisanje);
    },
    azurirajStavku(azuriranaStavka) {
      const index = this.stavke.findIndex(stavka => stavka.id === azuriranaStavka.id);
      if (index !== -1) {
        this.stavke[index] = azuriranaStavka;
      }
    },
  },
};
</script>

<style>

.container {
  background-color: #f0f0f0;
  padding: 20px;
  border: 1px solid #ccc;
}

.item-list {
  list-style: none;
  padding: 0;
}

.item-list li {
  margin: 10px 0;
}

.item-form input {
  width: 80%;
  padding: 5px;
  margin-right: 10px;
}

.item-form button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}

</style>
