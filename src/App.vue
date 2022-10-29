<template>
<div class="canva">
    <h1>Web terminal by MyQUENUM</h1>
        <div class="canva2">
            <div class="terminal">
                <div class="prompt">
                    <span id="prefix">myquenum@MyQ-localhost <span id="colon">:</span><span id="tilde">~</span> <span id="dollar">$</span></span> 
                    <input id="typing-zone" type="text" @keydown.enter="showHide" @keydown.backspace="dontDelete" @keydown.up="showOldCmd()" @keydown.down="showNextCmd()" v-model="fullCommand" autofocus>
                </div>
                <p id="message">{{message}}</p>
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
  name: 'HelloWorld',
  data() {
        return {
            fullCommand: "",
            message: "",
            boxIsVisible: false,
            index:null,
            commandStore: []
        }
    },
    methods: {
        showHide(){
            if(this.fullCommand == "sudo show my box" && this.boxIsVisible == false){
                this.boxIsVisible = true;
                this.message = "Box set as visible";
            }
            else if(this.fullCommand == "sudo hide my box" && this.boxIsVisible == true){
                this.boxIsVisible = false;
                this.message = "Box hidden";
            }else if(this.fullCommand == "sudo showHide my box"){
                if(!this.boxIsVisible)
                this.message = "Box set as visible";
                else
                this.message = "Box hidden";
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
                if(this.index == this.commandStore.length -1)
                  this.index++;
                this.fullCommand = "";
              } 
            }
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  *{
      margin: 0;
      box-sizing: border-box;
  }

  body{
    height: 100vh;
  }

  #app{
    height: 100%;
  }

  .canva{
      height: 100%;
      background-color: black;
  }

  h1{
      width: 100%;
      text-align: center;
      color: whitesmoke;
      font-family: sans-serif;
      font-size: 1.5rem;
  }

  .canva2{
      width: 100%;
      height: 95%;
      display: flex;
  }

  .terminal{
      height: 100%;
      width: 75%;
      background-color: #350a35;
      border: 1px solid whitesmoke;
  }

  .terminal:hover{
      border: 1px solid yellow;
  }

  .prompt{
    display: flex;
    gap: 5px;
    align-items: center;
  }

  #prefix{
    margin-left: 10px;
    color: rgb(98, 194, 9);
    font-weight: bold;
    font-family: Arial;
    font-size: 15px;
  }

  #colon{
    color: white;
  }

  #tilde{
    color: rgb(57, 57, 255);
  }

  #dollar{
    color: white;
  }
  input{
      background-color: #350a35;
      height: 40px;
      color: white;
      font-weight: bold;
      font-size: 15px;
      border: none;
  }

  input:focus{
      outline: none;
  }

  #message{
    margin-left: 10px;
    color: white;
    font-weight: bold;
    font-size: 15px;
    font-family: Arial; 
  }


  .monitor{
      width: 25%;
      height: 100%;   
      background-color: black;
      display: flex;
  }

  .screen{
      background-color: grey;
      width: 90%;
      height: 30%;
      margin: auto;
      justify-content: center;
      display: flex;
  }

  .box{
      width: 250px;
      height: 150px;
      background-color: red;
      margin: auto;
      justify-content: center;
  }

</style>
