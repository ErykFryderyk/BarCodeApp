<script setup>
import { reactive, ref } from 'vue';
import HelloWorld from './components/HelloWorld.vue'
import TheLabel from './components/TheLabel.vue'
import LabelsToPrint from './components/LabelsToPrint.vue'


const formData = ref({
  id: Math.random(),
  index: "LA89005W20KR",
  created: new Date().toLocaleDateString('en-GB'),
  name: "Złącze Superseal 2-pin kpl. męskie wtyczka z okablowaniem 20 cm",
  price: 15,
  unit: "PLN",
  quantity: "SZT"
})

const generatedLabales = ref([])
const isVisible = ref(true);

function addingLabelToArray() {
  if(generatedLabales.value.length < 28) {
    console.log(formData.value);
    generatedLabales.value.push(formData.value)
    // alert('Dodano nową etykietę')
    formData.value = {
      id: Math.random(),
      index: "LA89005W20KR",
      created: new Date().toLocaleDateString('en-GB'),
      name: "Złącze Superseal 2-pin....",
      price: 1,
      unit: "PLN",
      quantity: "SZT"
    }
  } else {
    alert("Limit etykiet na stronę!")
    return;
  }
}

function removeLabelById(id) {
  const index = generatedLabales.value.findIndex(label => label.id === id);
  if (index !== -1) {
    generatedLabales.value.splice(index, 1);
  }
}

function printingPage() {
  if(isVisible.value) {
    isVisible.value = !isVisible.value;
    setTimeout(() => {
      window.print()
      isVisible.value = !isVisible.value;
    }, 200);
  } else {
    isVisible.value = !isVisible.value;
  }
}
</script>

<template>
  <div class="app">
    <div class="main">
      <div class="top-section" v-if="isVisible">
        <img style="width: 190px;" src="./assets//logo-customer-kramp.jpg" alt="">
        <h4 style="margin-top: 80px; margin-bottom:10px">PODGLĄD ETYKIETY</h4>
        <TheLabel :data="formData"/>
      </div>
      <div class="main-section" v-if="isVisible">
        <h4 style="margin-bottom: 20px;">WYPEŁNIJ POLA</h4>
        <form class="form"@submit.prevent="addingLabelToArray">
          <div class="form-text-field">
            <input type="text" v-model="formData.index" required="" autocomplete="off">
            <label>Index</label>
          </div>
          <div class="form-text-field">
            <input type="text" v-model="formData.name" maxlength="120"required="" autocomplete="off">
            <label>Nazwa</label>
          </div>
          <div class="form-text-field">
            <input type="text" v-model="formData.price" required="" autocomplete="off">
            <label>Cena</label>
          </div>
          <div class="select-input">
            <label for="price">Waluta</label>
            <select id="price" v-model="formData.unit">
              <option value="PLN">PLN</option>
              <option value="EUR">EUR</option>
            </select>
          </div>
          <div class="select-input">
            <label for="quantity">Ilość na:</label>
            <select id="quantity" v-model="formData.quantity">
              <option value="SZT">SZT</option>
              <option value="OPA">OPA</option>
            </select>
          </div>
          <button type="submit">Dodaj Etykiete</button>
        </form>
      </div>
    </div>
    <div v-if="generatedLabales.length !== 0" class="result-section">
      <h2 v-if="isVisible">Podgląd wydruku:</h2>
      <button v-if="isVisible" style="margin-bottom: 10px" @click="printingPage()">
        <span v-if="isVisible">Drukuj etykiety</span>
        <!-- <span v-else>Edytuj wydruk</span> -->
      </button>
      <LabelsToPrint :labels="generatedLabales" @remove-label="removeLabelById"/>
    </div>
    <div v-else class="result-section">
      <h2>BRAK WYGENEROWANYCH ETYKIET</h2>
      <h5>Musisz dodać etykiete :)</h5>
    </div>
  </div>
</template>

<style scoped>
h2 {
  margin-bottom: 10px;
}

button {
  cursor: pointer;
  border-radius: 0.5rem;
  border: 1px solid #aaa;
  background-color: #fbfbfb;
  box-sizing: border-box;
  color: rgba(51, 65, 85, 1);
  padding: 10px;
  font-size: 14px;
  font-weight: 600;
  transition: background-color .2s ease-in-out;
  text-transform: uppercase;

  &:hover {
    background-color: #e0e0e0;
  }
}

.main{
  width: 100%;
  display: flex;
  justify-content: center;
  gap: 70px;

}
.top-section, .main-section{
  /* width: 100%; */
  margin-top: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #f8f8f8;
  padding: 10px 40px;
  border-radius: 5px;
  box-shadow: 0 0 7px 0px black;
}

.form{
  max-width: 500px;
  display: flex;
  flex-direction: column;
}
.form input, .form select, .form textarea {
  margin-bottom: 20px;
}

/* FORM INPUT */
.form-text-field {
  width: 100%;
  position: relative;
}

.form-text-field input {
  font-size: 100%;
  padding: 0.5em;
  outline: none;
  border: 2px solid rgb(200, 200, 200);
  background-color: transparent;
  border-radius: 10px;
  width: 100%;
}

.form-text-field label {
  font-size: 100%;
  position: absolute;
  left: 0;
  padding: 0.6em;
  margin-left: 0.5em;
  pointer-events: none;
  transition: all 0.3s ease;
  color: rgb(100, 100, 100);
}

.form-text-field :is(input:focus, input:valid)~label {
  transform: translateY(-60%) scale(.9);
  margin: 0em;
  margin-left: 0.8em;
  padding: 0.4em;
  background-color: #f8f8f8;
}

.form-text-field :is(input:focus, input:valid) {
  border-color: #686868;
}

/* SELECT INPUT */
.select-input{
  width: 100%;
  position: relative;
}
.select-input select {
  font-size: 100%;
  padding: 0.5em;
  outline: none;
  border: 2px solid rgb(200, 200, 200);
  background-color: transparent;
  border-radius: 10px;
  width: 100%;
}
.select-input label{
  font-size: 100%;
  position: absolute;
  left: 0;
  padding: 0.6em;
  margin-left: 0.5em;
  pointer-events: none;
  transition: all 0.3s ease;
  transform: translateY(-60%) scale(.9);
  color: rgb(100, 100, 100);
  margin-left: 0.8em;
  padding: 0.4em;
  background-color: #f8f8f8;
}
.select-input :is(input:focus, input:valid)~label {
  transform: translateY(-60%) scale(.9);
  margin: 0em;
  margin-left: 0.8em;
  padding: 0.4em;
  background-color: #f8f8f8;
}

.select-input :is(select:focus, select:valid) {
  border-color: #686868;
}
.result-section {
  margin-top: 70px;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
