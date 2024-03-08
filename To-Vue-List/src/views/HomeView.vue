<script>
export default {
  data() {
    return {
      nuovoItem: "",
      lista: []
    }
  },
  methods: {
    aggiungiItem() {
      if (this.nuovoItem.trim() !== "") {
        console.log(this.nuovoItem.trim());
        this.lista.push(this.nuovoItem.trim().toUpperCase());
        console.log(this.lista);
        this.nuovoItem = "";
      } else {
        alert("non hai aggiunto nulla")
      }
    },
    rimuoviItem(indice) {
      this.lista.splice(indice, 1);
      console.log(this.lista);
    },
    modificaItem(indice) {
      const edit = prompt("Modifica l'oggetto");
      if (edit.trim() !== "") {
        this.lista[indice] = edit.toUpperCase()
      } else {
        alert("Non hai inserito un valore")
      }
    },
    eliminaLista() {
      this.lista = []
    }
  }
}
</script>

<template>
  <main>
    <h1 class="text-center text-3xl text-[#34495d] my-10">To-<span class="text-[#00b36b]">Vue</span> List</h1>
    <div class="bg-[#34495d] text-[#00b36b] rounded-3xl mx-[600px] min-h-80 py-[30px]">
      <div class="flex justify-center gap-3">
        <input class="border border-[#00b36b] rounded-lg bg-[#34495d] text-white" type="text" v-model="nuovoItem"
          @keyup.enter="aggiungiItem" placeholder="  Nuovo elemento..">
        <button @click="aggiungiItem">Aggiungi alla lista</button>
      </div>
      <div class="px-[40px] mt-5">
        <ul>
          <li v-for="(items, indice) in lista" class="flex justify-between mb-2 border-b">
            <p class="text-white"> {{ items }}</p>
            <div class="w-[150px] flex justify-between">
              <button @click="rimuoviItem(indice)">Rimuovi</button>
              <button @click="modificaItem(indice)">Modifica</button>
            </div>

          </li>
        </ul>
      </div>
      <div class="flex justify-center items-center mt-4">
        <button @click="eliminaLista" class="">Elimina la lista</button>
      </div>
    </div>
  </main>
</template>