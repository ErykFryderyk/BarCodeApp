<script setup>
import TheBarcode from './TheBarcode.vue';

const props = defineProps({
    labels: Array,
})

</script>
<template>
    <div class="page-a4">
        <div style="position: relative;" v-for="label in labels" class="label" alt="Kliknij na etykietę jeżeli chcesz ją usunąć" @click="$emit('removeLabel',label.id)">
            <svg class="trash-icon" xmlns="http://www.w3.org/2000/svg" shape-rendering="geometricPrecision" text-rendering="geometricPrecision" image-rendering="optimizeQuality" fill-rule="evenodd" clip-rule="evenodd" viewBox="0 0 456 511.82"><path fill="#9e4646" d="M48.42 140.13h361.99c17.36 0 29.82 9.78 28.08 28.17l-30.73 317.1c-1.23 13.36-8.99 26.42-25.3 26.42H76.34c-13.63-.73-23.74-9.75-25.09-24.14L20.79 168.99c-1.74-18.38 9.75-28.86 27.63-28.86zM24.49 38.15h136.47V28.1c0-15.94 10.2-28.1 27.02-28.1h81.28c17.3 0 27.65 11.77 27.65 28.01v10.14h138.66c.57 0 1.11.07 1.68.13 10.23.93 18.15 9.02 18.69 19.22.03.79.06 1.39.06 2.17v42.76c0 5.99-4.73 10.89-10.62 11.19-.54 0-1.09.03-1.63.03H11.22c-5.92 0-10.77-4.6-11.19-10.38 0-.72-.03-1.47-.03-2.23v-39.5c0-10.93 4.21-20.71 16.82-23.02 2.53-.45 5.09-.37 7.67-.37zm83.78 208.38c-.51-10.17 8.21-18.83 19.53-19.31 11.31-.49 20.94 7.4 21.45 17.57l8.7 160.62c.51 10.18-8.22 18.84-19.53 19.32-11.32.48-20.94-7.4-21.46-17.57l-8.69-160.63zm201.7-1.74c.51-10.17 10.14-18.06 21.45-17.57 11.32.48 20.04 9.14 19.53 19.31l-8.66 160.63c-.52 10.17-10.14 18.05-21.46 17.57-11.31-.48-20.04-9.14-19.53-19.32l8.67-160.62zm-102.94.87c0-10.23 9.23-18.53 20.58-18.53 11.34 0 20.58 8.3 20.58 18.53v160.63c0 10.23-9.24 18.53-20.58 18.53-11.35 0-20.58-8.3-20.58-18.53V245.66z"/></svg>
            <div class="top-part">
                <p id="index" class="index">{{ label.index }}</p>
                <p id="date" class="date">{{ label.created }}</p>
            </div>
            <h4 id="index-name" class="index-name">{{ label.name }}</h4>
            <div class="center-part">
                <p id="price" class="price">{{ label.price }}</p>
                <span id="unit" class="unit"><b>{{ label.unit }}</b> w tym <b>23%</b> VAT</span>
            </div>
            <!-- <div class="bottom-part">
                <p class="text"></p>
                <p id="additional-price" class="additional-price"></p>
                <p id="currency" class="currency"></p>
            </div> -->
            <div class="barcode-container">
                <TheBarcode :value="label.index"/>
            </div>
            <p class="quantity">{{ label.quantity }}</p>
        </div>
    </div>
</template>


<style scoped>
.page-a4 {
    width: 200mm;
    max-height: calc(7 * 37mm);
    display: flex;
    flex-wrap: wrap;
    background: #fff;
    box-shadow: 0 0 7px 0px white;
}
.label {
    width: 50mm;
    height: 37mm;
    padding: 5px;
    background-color: #fff;
    /* border: 1px dotted black; */
    cursor: pointer;
}
.label:hover{
    background-color: #e8e8e8;
}
.trash-icon {
    position: absolute; 
    width: 50px; 
    left: 50%; 
    top: 50%; 
    transform: translate(-50%, -50%); 
    z-index: 99;
    opacity: 0;
    transition: .1s ease;
}
.label:hover .trash-icon {
    opacity: 1;
}
.top-part {
    display: flex;
    justify-content: space-between;
    margin-bottom: 5px;
}

.center-part {
    display: flex;
    justify-content: end;
}

.bottom-part {
    max-height: 10px;
    display: flex;
    justify-content: center;
    margin-bottom: 5px;
}

.index {
    margin-left: 5px;
    font-size: 10px;
    font-weight: bold;
}

.date {
    font-size: 10px;
}

.index-name {
    height: 25px;
    font-size: 10px;
    text-align: center;
    font-weight: normal;
    margin-bottom: 5px;
}

.price {
    font-size: 20px;
    font-weight: bold;
}

.unit {
    max-height: 25px;
    margin-left: 5px;
    font-size: 7px;
    font-weight: bold;
    transform: translateY(11px);
}

.text,
.additional-price,
.currency {
    font-size: 7px;
    margin-right: 2px;
    height: 7px;
}
.barcode128 {
font-family: 'Libre Barcode 128 Text';
    font-size: 30px;
    margin-bottom: -12px;
}
.barcode-container {
    width: 100%;
    height: 50px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.barcode-text {
    font-size: 7px;
}
.quantity{
    text-align: right;
    font-size: 8px;
}
</style>