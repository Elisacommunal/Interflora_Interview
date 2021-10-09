<template>
    <div class="card">
        <div class="card-title">
            <h1>Test API</h1>
            <p>J'ai choisi une API avec des chats</p>
            <!-- Button call function randomName() -->
            <button @click="randomName()" class="card--btn"><i class="fas fa-paw"></i> My name <i class="fas fa-paw"></i> </button>
            <div >
            <!-- Show the name -->
            <p class="name"> {{dataName}} </p>
            </div>
            <!-- Button call function randomImage() -->
            <button @click="randomImage()" class="card--btn"><i class="fas fa-paw"></i> Meow <i class="fas fa-paw"></i> </button>
        </div>
        <!-- If there is data in 'dataCats', display it here  -->
        <div v-if="dataCats" v-for="item in dataCats" :key="item.id">
            <img class="card--image" v-if="item.url" :src="item.url">
        </div>
        <!-- Else we display the default image  -->
        <div v-else>
            <img class="card--image" src="../assets/Cat.jpg">
        </div>
    </div>
    <!--MODAL-->
    <transition name="modal-fade" v-show="isModalVisible">
    <div class="modal-backdrop">
        <div class="modal">
        <!-- modal header -->
        <header class="modal-header">
            <slot name="header">Meow !</slot>
            <button type="button" class="btn-close" @click="closeModal()">x</button>
        </header>
        <!-- modal body -->
        <section class="modal-body">
            <slot name="body">Voulez-vous voir un nouveau chat ?</slot>
        </section>
        <!-- modal footer -->
        <footer class="modal-footer">
            <slot name="footer">Si oui clique en dessous</slot>
            <!-- Button call function randomImage() -->
            <button type="button" class="btn-green" @click="randomImage()"><i class="fas fa-paw"></i> Oui <i class="fas fa-paw"></i></button>
        </footer>
        </div>
    </div>
</transition>
    
</template>
<script>
// Add axios for communicate with API
import axios from "axios";
// Const for call 'cat-name'
const catNames = require('cat-names');

export default {
    name: 'Home',
    data(){
        return {
            dataCats: '',
            isModalVisible: "",
            // Function to set up the 25s timer modal
            TimeOut: setTimeout(function(){ 
              this.isModalVisible = true; 
              }.bind(this), 25000),
            dataName : catNames.random()
        }
    },
    methods: {
        // Function that recovers random photos
        randomImage(){
            // If there is a modal opened we hide it
            this.isModalVisible = false;
            // We call the API with axios
            axios.get('https://api.thecatapi.com/v1/images/search', {
                method: 'GET',
                })
            .then((response) => {
              // We add the response in data 'dataCats'
                this.dataCats = response.data;
                // Function to set up the 25s timer
                setTimeout(function(){ 
                  this.isModalVisible = true; 
                  }.bind(this), 25000)
            })   
        },
        // Function that recovers random names
        randomName(){
          this.dataName= catNames.random();
        },
        // Function that shows the modal
        showModal() {
        this.isModalVisible = true;
        },
        // Function that closes the modal
        closeModal() {
          this.isModalVisible = false;
        },
    }
}
</script>
<style>
/* --- Layout of the card --- */ 
.card{
    display: block;
    margin-left: auto;
    margin-right: auto;
    padding: 20px;
    width: 600px;
    background-color: #529b7734;
    border-radius: 15px;
}
.card--image{
    display: block;
    margin-left: auto;
    margin-right: auto;
    width: 500px;
    margin-bottom: 25px;
    height: 500px;
    object-position: 50% 50% ;
    object-fit: cover;
    border-radius: 75px;
    box-shadow: gray 5px 5px 35px;
    }

.card--btn{
    width: 200px;
    margin: 20px 0;
    padding: 10px;
    border: none;
    color: #ffffff;
    background-color: #529B76;
    box-shadow: gray 5px 5px 35px;
    cursor: pointer;
    border-radius: 5px;
}

.card-title{
    width: 200px;
    text-align: center;
    display: block;
    margin-left: auto;
    margin-right: auto;
}

.name{
  font-size: 35px;
  font-weight: 600;
  padding: 0;
  margin: 0;
}

/* --- Layout of the Modal --- */ 

.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(60, 68, 61, 0.486);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background: #ffffff;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
  border-radius: 5px;
}

.modal-header,
.modal-footer {
  padding: 15px;
  display: flex;
}

.modal-header {
  position: relative;
  border-bottom: 1px solid #eeeeee;
  color: #529B76;
  font-size: 20px;
  font-weight: 600;
  justify-content: space-between;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
  flex-direction: column;
  justify-content: flex-end;
}

.modal-body {
  position: relative;
  padding: 10px 10px;
}

.btn-close {
  position: absolute;
  top: 0;
  right: 0;
  border: none;
  font-size: 20px;
  padding: 10px;
  cursor: pointer;
  font-weight: bold;
  color:#529B76;
  background: transparent;
}

.btn-green {
  color: white;
  background: #529B76;
  border: 1px solid #529B76;
  border-radius: 5px;
  cursor: pointer;
}

/* --- Modal transition --- */ 

.modal-fade-enter,
.modal-fade-leave-to {
  opacity: 0;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 1s ease;
} 


@media screen and (max-width: 640px) {
    .card{
      background-color: transparent !important; 
      width: 260px;
      padding: 0;
    }
    .card--image{
    display: block;
    margin-left: auto;
    margin-right: auto;
    width: 250px;
    margin-bottom: 25px;
    height: 250px;
    object-position: 50% 50% ;
    object-fit: cover;
    border-radius: 75px;
    box-shadow: gray 5px 5px 35px;
    }
}

</style>