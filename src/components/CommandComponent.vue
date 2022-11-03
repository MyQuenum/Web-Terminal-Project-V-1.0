<template>
 <div>
    <div class="flex">
    <p>myquenum@MyQ-localhost:~$ </p>
    <input type="text" @keydown.enter="showHide" @keydown.backspace="dontDelete" @keydown.up="showOldCmd()" @keydown.down="showNextCmd()" v-model="fullCommand" >
  </div>
 </div>
</template>

<script>
export default {
    data(){
        return{
            fullCommand: ""
        }
    },


    showHide(){
            if(this.fullCommand == "sudo show my box" && this.boxIsVisible == false){
                this.boxIsVisible = true;
            }
            else if(this.fullCommand == "sudo hide my box" && this.boxIsVisible == true){
                this.boxIsVisible = false;
            }else if(this.fullCommand == "sudo showHide my box"){
                this.boxIsVisible = !this.boxIsVisible;
            }
            this.upIndex = 0;
            this.commandStore.push(this.fullCommand);
            this.fullCommand="";
            this.index = null;
        },
        showOldCmd(){
            if (this.index == null) {
                this.index = this.commandStore.length;
            }
            if(this.commandStore != [] && this.index >= 1){ 
                this.index--;
                this.fullCommand = this.commandStore[this.index];
            }else{
                this.fullCommand = "";
            }
        },
        showNextCmd(){
            if (this.index == null) {
              this.fullCommand = "";
            }else{
              if (this.commandStore != [] && this.index < this.commandStore.length - 1) {
                this.index++;
                this.fullCommand = this.commandStore[this.index];
              }else{
                this.fullCommand = "";
              } 
            }
        }
}
</script>

<style src="../styles/App.css">
    
</style>