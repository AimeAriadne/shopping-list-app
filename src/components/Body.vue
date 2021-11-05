<template>
    <div 
        v-if="editing" 
        id="wrapper" 
    >   
        <button 
            :disabled="newItem.length < 3" 
            @click="addItem(newItem)">
            <img id="add" :src="addIcon">
        </button>
        <div>
            <input 
                v-model="newItem" 
                @keyup.enter="addItem(newItem)" 
                id="new-item" 
                maxlength="20"
                placeholder="Add a new item" 
                type="text" 
            >
            <span id="char-count">{{newItemchar}}/20</span>
        </div>
        
        <label 
        v-if="editing" 
        id="priority"
    >
        <input 
            id="check"
            v-model="newItemHighPriority"
            type="checkbox"
        >
        <span>Priority</span>
    </label>
    </div>

    

    <br>
    <br>

    <p v-if="items.length === 0">{{ msg }}</p>

    <ul>
        <li 
            v-for="(item, index) in items"
            :key="`item-${index}`"
            :class="{ bought: item.purchased }"
        >
            <span 
            :class="{ important: item.priority }"
            @click="purchasedItem(index)"
            >
            {{ item.label }} 
            </span>
            <button 
                class="remove" 
                @click="removeItem(index)"
            >
                <img src="../assets/lixo.svg"/>
            </button>
        </li>
    </ul>
</template>

<script>
export default {
    name: 'Body',
    props: {
        editing: Boolean
    },
    data() {
        return {
            msg: 'Nothing to buy! Add new items.',
            addIcon: 'https://img.icons8.com/material-sharp/24/000000/add.png',
            newItem: '',
            newItemHighPriority: false,
            items: (localStorage.getItem('items')) ? JSON.parse(localStorage.getItem('items')) : []
        }
    },
    computed: {
        newItemchar() {
            return this.newItem.length
        }
    },
    methods: {
        addItem(item) {
            this.items.splice(0, 0, {label: item, purchased: false, priority: this.newItemHighPriority})
            this.newItemHighPriority = false
            this.newItem = ''
            localStorage.setItem('items', JSON.stringify(this.items))
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

<style scoped>
#priority, #char-count {
    color: rgb(150, 148, 148);
    font-size: .7rem;
}



#wrapper, #priority {
    display: flex;
    align-items: center;
    justify-content: center;
}

#new-item {
  border: none;
  border-bottom: .1rem dashed gray;
  width: 9.5rem;
  text-align: center;
  background-color: transparent ;
}

#new-item:focus {
  outline: none;
}

img{
  height: 1.2rem;
}


ul {
  padding-left: 1.5rem;
  margin: 0;
}

li {
  padding: .2rem;
  cursor: pointer;
}

.bought{
  text-decoration: line-through;
  color: rgb(150, 148, 148);
}

.important {
  color: rgb(238, 101, 101);
}

@media (min-width: 720px) {
  #new-item {
    width: 12rem;
  }
}

</style>