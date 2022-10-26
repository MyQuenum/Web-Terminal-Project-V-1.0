<template>
<div class="canva">
    <h1>Web terminal by MyQUENUM</h1>
        <div class="canva2">
            <div class="terminal">
              <input type="text" @keydown.enter="showHide" @keydown.backspace="dontDelete" @keydown.up="showOldCmd()" @keydown.down="showNextCmd()" v-model="fullCommand"><br><br>
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
            fullCommand: "myquenum@MyQ-localhost:~$ ",
            boxIsVisible: false,
            index:null,
            commandStore: []
        }
    },
    methods: {
        showHide(){
            if(this.fullCommand == "myquenum@MyQ-localhost:~$ sudo show my box" && this.boxIsVisible == false){
                this.boxIsVisible = true;
            }
            else if(this.fullCommand == "myquenum@MyQ-localhost:~$ sudo hide my box" && this.boxIsVisible == true){
                this.boxIsVisible = false;
            }else if(this.fullCommand == "myquenum@MyQ-localhost:~$ sudo showHide my box"){
                this.boxIsVisible = !this.boxIsVisible;
            }
            this.upIndex = 0;
            this.commandStore.push(this.fullCommand);
            this.fullCommand="myquenum@MyQ-localhost:~$ ";
            this.index = null;
        },
        dontDelete(){
            if(this.fullCommand == "myquenum@MyQ-localhost:~$ ")
            {
                this.fullCommand = "myquenum@MyQ-localhost:~$  ";
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
                this.fullCommand = "myquenum@MyQ-localhost:~$ ";
            }
        },
        showNextCmd(){
            if (this.index == null) {
              this.fullCommand = "myquenum@MyQ-localhost:~$ ";
            }else{
              if (this.commandStore != [] && this.index < this.commandStore.length - 1) {
                this.index++;
                this.fullCommand = this.commandStore[this.index];
              }else{
                this.fullCommand = "myquenum@MyQ-localhost:~$ ";
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

  input{
      background-color: #350a35;
      width: 100%;
      height: 50px;
      color: rgb(207, 207, 77);
      font-weight: bold;
      border: none;
  }

  input:focus{
      outline: none;
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
