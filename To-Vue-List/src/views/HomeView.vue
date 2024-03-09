<script>
export default {
  data() {
    return {
      nuovoItem: "",
      lista: [],
      show: true,
      voidInput: false
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
        this.voidText()
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
        this.voidText()
      }
    },
    eliminaLista() {
      this.lista = []
    },
    isEmpty() {
      if (this.lista.length == 0) {
        this.show = false
      } else if (this.lista.length >= 1) {
        this.show = true
      }
    },
    voidText() {
      this.voidInput = !this.voidInput
      setTimeout(() => {
        this.voidInput = !this.voidInput
      }, 2000);
    }
  },
  mounted() {
    this.isEmpty()
  },
  updated() {
    this.isEmpty()
  }
}
</script>

<template>
  <main class="bg-[#F9FBE7] h-screen w-full">
    <h1 class="text-center text-3xl text-[#34495d] pt-10 mb-10">To-<span class="text-[#00b36b]">Vue</span> List</h1>
    <div class="bg-[#34495d] text-[#00b36b] rounded-3xl mx-[600px] min-h-80 py-[30px] border-4 border-[#1c2731]">
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
      <div class="flex justify-center items-center mt-4" v-show="show">
        <button @click="eliminaLista" class="">Elimina la lista</button>
      </div>
      <div v-show="voidInput" class="flex justify-center items-center mt-10">
        <p class="p-5 text-red-600 bg-red-300 text-[18px] rounded-xl">Non hai inserito un valore</p>
      </div>
    </div>
  </main>
</template>