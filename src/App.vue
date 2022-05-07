<template>
  <div :class="[{flexStart : step === 1},'wrapper']">

    <Transition name = "slide">
      <img src="./assets/logo.svg" class="logo" v-if="step === 1" @click="step = 0">
    </Transition>

    <Transition name="fade">
      <HeroImage v-if="step === 0"/>
    </Transition>

    <Claim v-if="step === 0"/>
    <Search :value="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="lds-ring" v-if="step === 1 && loading"><div></div><div></div><div></div><div></div></div>

    <Transition name = "fade">
      <div class="results" v-if="results && !loading && step === 1 ">
        <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click="handleModalOpen(item)"/>
      </div>
    </Transition>

    <Transition name = "modal">
      <Modal v-if="modalOpen" :item="modalItem" @close-modal = "this.modalOpen = false;"/>
    </Transition>

  </div>
</template>

<script>
import Claim from '@/components/Claim.vue';
import Search from '@/components/Search.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

import axios from 'axios';
const API = "https://images-api.nasa.gov/search";

let debounceTime = 1.5;
let debounce;

export default {

  name: 'App',

  data () {
    return {
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
      modalOpen: false,
      modalItem: null,
    }
  },

  methods: {
    handleInput (e) {

      this.searchValue = e.target.value;

      clearTimeout(debounce);
      debounce = null;
      if(this.searchValue !== '')
        debounce = setTimeout(() => {
          this.loading = true;
          axios.get(`${API}?q=${this.searchValue}&media_type=image`)
            .then((response)=>{
              console.log(response.data.collection.items);
              this.results = response.data.collection.items;
              this.loading = false;
              this.step = 1;
            })
            .catch((error) => {
              console.log(error);
            });
        },debounceTime*1000)

    },

    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },

  },

  components:{
    Claim,
    Search,
    HeroImage,
    Item,
    Modal
  }
}
</script>

<style type="text/css">
  *{
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  body{
    font-family: 'Montserrat', sans-serif;
    margin: 0; 
    padding: 0; 
  }
</style>

<style lang="scss" scoped>
 @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@200;300;400;600;800&display=swap');

.fade-enter-active, 
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from, 
.fade-leave-to {
  opacity: 0;
}

.slide-enter-active, .slide-leave-active {
  transition: margin-top .3s ease;
}

.slide-enter-from, .slide-leave-to {
  margin-top: -50px;
}

.modal-enter-active, .modal-leave-active {
  transition: all .5s ease;
}

.modal-enter-from, .modal-leave-to {
  transform:scale(0.1);
  opacity: 0;
}

.wrapper
{
  position: relative;
  color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 0;
  height: 100vh;
  min-height: 100vh;
  padding: 30px;
  width: 100%;
  background-color: rgba(0,0,0,0);

  &.flexStart{
    justify-content: flex-start;
  }
}

.logo
{
  position: absolute;
  top: 15px;
  width: 50px;
  cursor: pointer;
}

.results
{
  width: 90%;
  margin-top: 50px;
  color: #000;
  display: grid;
  grid-template-columns: 1fr;
  grid-gap: 20px;

  @media (min-width: 575px){
    grid-template-columns: 1fr 1fr;
  }

  @media (min-width: 768px) {
    grid-template-columns: 1fr 1fr 1fr;
  }

  @media (min-width: 1500px) {
    grid-template-columns: 1fr 1fr 1fr 1fr;
  }
}

  .lds-ring {
    margin-top: 100px;
    display: block;
    width: 80px;
    height: 80px;
    padding: relative;
  }
  .lds-ring div {
    box-sizing: border-box;
    display: block;
    position:absolute;
    width: 64px;
    height: 64px;
    margin: 8px;
    border: 8px solid #1e3d4a;
    border-radius: 50%;
    animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
    border-color: #1e3d4a transparent transparent transparent;
  }
  .lds-ring div:nth-child(1) {
    animation-delay: -0.45s;
  }
  .lds-ring div:nth-child(2) {
    animation-delay: -0.3s;
  }
  .lds-ring div:nth-child(3) {
    animation-delay: -0.15s;
  }
  @keyframes lds-ring {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

</style>
