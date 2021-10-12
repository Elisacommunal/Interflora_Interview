<template>
    <div class="card">
        <div class="card-title">
            <h1>🎲😸<br>Cats name and photo randomizer<br>😸🎲</h1>
            <p> Here is my project : <br>
                It allows you to find a name for each cat. <br>
                You can choose to edit either the name or the photo.
            </p>
            <p> The API I used for cat photos is this:</p>
            <a href=" https://api.thecatapi.com/v1/images/search">Click here</a>
            <p> As requested you will see a 25s modal appear after a request for a new photo.</p>
            <p> For the cat names I used the "cat-names" dependency which allows you to have random names.</p>
            <p> This project was carried out with Vue 3 and without a CSS framework</p>
            <p> Take a look !</p>
            <!-- Button call function randomName() -->
            <button @click="randomName()" class="card--btn"><i class="fas fa-paw"></i> Cat name <i class="fas fa-paw"></i> </button>
            <div >
            <!-- Show the name -->
            <p class="name"> {{dataName}} </p>
            </div>
            <!-- Button call function randomImage() -->
            <button @click="randomImage()" class="card--btn"><i class="fas fa-paw"></i> Meow <i class="fas fa-paw"></i> </button>
        </div>
        <!-- If there is data in 'dataCats', display it here  -->
       <!--  <div v-if="dataCats" v-for="item in dataCats" :key="item.id">
            <img class="card--image" v-if="item.url" :src="item.url">
        </div> -->
        <div v-if="dataCats">
            <img class="card--image" :src="dataCats[0].url">
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
            <slot name="body">Do you want to see a new cat ?</slot>
        </section>
        <!-- modal footer -->
        <footer class="modal-footer">
            <slot name="footer">If yes click below</slot>
            <!-- Button call function randomImage() -->
            <button type="button" class="btn-green" @click="randomImage()"><i class="fas fa-paw"></i> Yes <i class="fas fa-paw"></i></button>
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
       async randomImage(){
            // If there is a modal opened we hide it
            this.isModalVisible = false;
            clearTimeout(this.TimeOut)
            // We call the API with axios
           const response = await axios.get ('https://api.thecatapi.com/v1/images/search')
              // We add the response in data 'dataCats'
                this.dataCats = await response.data;
                // Function to set up the 25s timer
                  this.TimeOut = setTimeout(function(){ 
                  this.isModalVisible = true; 
                  }.bind(this), 25000)
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
    width: 400px;
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
    .card-title{
    width: 200px;
    font-size: 14px;
    text-align: center;
    display: block;
    margin-left: auto;
    margin-right: auto;
}
}

</style>