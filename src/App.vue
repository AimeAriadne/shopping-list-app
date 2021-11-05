<template>
  <div class="container">
    <Header 
      :editing="editing"
      @do-not-edit="doEdit(false)"
      @do-edit="doEdit(true)" 
      />

    <Body :editing="editing"/>
  </div>

  <Footer />
</template>

<script>
import Header from './components/Header.vue'
import Body from './components/Body.vue'
import Footer from './components/Footer.vue'
export default {
  name: 'App',
  components: {
    Header,
    Body,
    Footer
  },
  data() {
    return {
      editing: false,
    }
  },
  methods: {
    doEdit(state){
      this.editing = state
    }
  }
}
</script>

<style>
body{
    background-image: url('./assets/background.jpg');
    background-color: rgba(223, 239, 247, 0.9);
    background-blend-mode: lighten;
    min-height: 20rem;
    margin: 0;
    
}

#app {
  font-family: 'Courier New', Courier, monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  
}

.container {
    background: rgb(223, 239, 247);
    border-radius: .2rem;
    box-shadow: .2rem .2rem rgba(0, 0, 0, 0.2);
    width: 80%;
    padding: .5rem;
    margin: 0;
    max-width: 30.5rem;
    position: absolute;
    top: 50%;
    left: 50%;
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
}

button {
  padding: 0;
  border:none;
  border-radius: .3rem;
  cursor: pointer;
  background-color: transparent;
  color: white;
}

button:disabled {
  opacity: 0;
}

.btn-new{
  background-color: rgb(142, 189, 221);
  border: none;
  padding: .5rem;
}

.btn-cancel {
  background-color: rgb(238, 101, 101);
  border: none;
  padding: .5rem;
}

.remove{
  margin-right: 0;
  float:right;
  background-color: transparent;
  border: none;
}

@media (max-width: 370px) {
  .container{
    min-width: 18rem;
    top: 30%;  
  }
}
</style>
