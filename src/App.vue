<template>
<div class="canva">
    <h1>Web terminal by MyQUENUM</h1>
        <div class="canva2">
            <div class="terminal flex">
               <p>myquenum@MyQ-localhost:~$</p>
              <input class="inputHeigt" type="text" @keydown.enter="execution"  @keydown.up="showOldCmd()" @keydown.down="showNextCmd()" v-model="fullCommand" ><br><br>
              <!-- <command-component /> -->
            </div>
            <div class="monitor">
                <div class="screen">
                  <div class="box" v-if="boxIsVisible == true"></div>
                </div>
            </div>
        </div>
  </div>
</template>

<script>
export default {
  data() {
        return {
            fullCommand: "",
            boxIsVisible: false,
            index:null,
            commandStore: []
        }
    },
    components:{
        
    },
    methods: {
        execution(){
            const firstCommand = this.splitCommand()[0];
            const commandParam = this.splitCommand()[1]
            switch(firstCommand){
                case 'show':
                    this.showBox(commandParam);
                    break;
                case 'hide':
                    this.hideBox(commandParam);
                    break;
                case 'color':

                    break;
                default :

                break
            }
            this.upIndex = 0;
            this.commandStore.push(this.fullCommand);
            this.fullCommand="";
            this.index = null;
        },

        showBox(param){
            if(param == "box"){
                this.boxIsVisible = true;
            }
        },
        hideBox(param){
            if(param == "box"){
                this.boxIsVisible = false;
            }
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
        },
        splitCommand(){
            return this.fullCommand.split(' ');
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style src="./styles/App.css">
  
</style>
