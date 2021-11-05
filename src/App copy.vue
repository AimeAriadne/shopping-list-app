<template>

  <div id="header">
  <h1>{{ header }}</h1>
  <button v-if="editing" @click="doEdit(false)" class="btn-cancel">Cancel</button>
  <button v-else @click="doEdit(true)" class="btn-new">New Items</button>
  </div>

  <div v-if="editing" id="wrapper">
  <div>
    <input id="new-item" v-model="newItem" @keyup.enter="addItem(newItem)" placeholder="Add a new item" type="text" maxlength="20">
    <span id="char-count">{{newItemchar}}/20</span>
  </div>
  <button :disabled="newItem.length < 3" @click="addItem(newItem)"><img :src="addIcon"></button>
  </div>
  
  <label v-if="editing" id="priority">
      <input v-model="newItemHighPriority" type="checkbox">
      <span>Priority</span>
  </label>

  <br><br>

  <p v-if="items.length === 0">{{ msg }}</p>
  
  <ul>
    <li
      v-for="(item, index) in items"
      :key="`item-${index}`"
      :class="{ bought: item.purchased }"
    >
      <span @click="purchasedItem(index)" :class="{ important: item.priority }">
        {{ item.label }} 
      </span>
      <button class="remove" @click="removeItem(index)">
        <img src="./assets/lixo.svg"/>
      </button>
    </li>

  <footer>
    <p>Icons by 
      <a href="https://icons8.com/icon/EINqUt4JSfeM/adicionar">Icons8</a>
    </p>
    </footer>
</template>

<script>

export default {
  name: 'App',
   data() {
    return {
      header: 'Shopping List App',
      msg: 'Nothing to buy! Add new items.',
      addIcon: 'https://img.icons8.com/material-sharp/24/000000/add.png',
      newItem: '',
      editing: false,
      newItemHighPriority: false,
      items: (localStorage.getItem('items')) ? JSON.parse(localStorage.getItem('items')) : []
    }
  },
  computed: {
    newItemchar() {
      return this.newItem.length
    },
    reverseItems() {
      return [...this.items].reverse()
    },
  },
  methods: {
    addItem(item) {
      this.items.splice(0, 0, {label: item, purchased: false, priority: this.newItemHighPriority})
      this.newItemHighPriority = false
      this.newItem = ''
      localStorage.setItem('items', JSON.stringify(this.items))
    },
    doEdit(state){
      this.editing = state
      this.newItemHighPriority = false
      this.newItem = ''
    },
    removeItem(pos){
      this.items.splice(pos, 1)
      this.newItemHighPriority = false
      this.newItem = ''
      localStorage.setItem('items', JSON.stringify(this.items))
    },
    purchasedItem(pos) {
      this.items[pos].purchased = !this.items[pos].purchased
      localStorage.setItem('items', JSON.stringify(this.items))
    }
  }
}
</script>

<style>
#app {
  font-family: 'Courier New', Courier, monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  background: white;
  width: 50%;
  padding: 1rem;
  border-radius: .2rem;
  box-shadow: .2rem .2rem rgba(0, 0, 0, 0.2);
  min-width: 17.5rem;
  max-width: 30.5rem;
  margin: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}
body{
    background: rgb(223, 239, 247);

}
ul {
  padding-left: 1.5rem;
  margin: 0;
}
li {
  padding: .2rem;
  cursor: pointer;
}

#new-item {
  margin-left: .5rem;
  border: none;
  border-bottom: .1rem dashed gray;
  width: 12rem;
  text-align: center;
}
#new-item:focus {
  outline: none;
}
button {
  border:none;
  border-radius: .3rem;
  cursor: pointer;
  background-color: transparent;
}

button:disabled {
  opacity: 0;
}
.btn-new{
  margin-right: 0;
  background-color: rgb(142, 189, 221);
  border: none;
  color: white;
  padding: .5rem;

}
.btn-cancel {
  margin-right: 0;
  background-color: rgb(238, 101, 101);
  color: white;
  border: none;
  padding: .5rem;
}
.remove{
  margin-right: 0;
  float:right;
  background-color: transparent;
  border: none;
}

img{
  height: 1.2rem;
}
#header {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}
.bought{
  text-decoration: line-through;
  color: rgb(150, 148, 148);
}

#priority, #char-count, #filter {
    color: rgb(150, 148, 148);
    font-size: .8rem;
}
#wrapper, #priority, #filter {
  display: flex;
  align-items: center;
  justify-content: center;
}
.important {
  color: rgb(238, 101, 101);
}
footer {
  background-color: white;
  color: #2c3e50;
  position: fixed;
}

@media (min-width: 600px) {
  #new-item {
    width: 15rem;
  }
}
</style>
