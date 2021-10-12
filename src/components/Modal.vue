<template>
    <!--MODAL-->
    <!-- <transition name="modal-fade" v-if="isModalVisible"> -->
     <div class="modal-backdrop">
        <div class="modal">
        <!-- modal header -->
        <header class="modal-header">
            <slot name="header">Meow !</slot>
            <button type="button" class="btn-close" @click="test()">x</button>
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
<!-- </transition> -->
</template>
<script>

export default {
    data(){
        return{
            isModal: "",
        }
    },
    methods: {
        // Function that shows the modal
        showModal() {
            this.isModalVisible = true;
        },
        // Function that closes the modal
        closeModal() {
          this.isModalVisible= false;
        },
        test(){
            this.isModal= false
        }
    }
}
</script>
<style>
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

.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 1s ease;
} 
</style>