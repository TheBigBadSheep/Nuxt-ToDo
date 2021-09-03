<template>
    <div class="container">    
        <header class="Title">
            To Do's
        </header>
        

    <div>
        <input class="InputBox" type="text" v-model="item" @keypress.enter="add" placeholder="Your text goes here!">
        <button class="Button" @click="add"> Submit </button>
        
        <div class="Column">
            <ul class= "List">
                <li class="Items" v-for="(item, index) in items" :key="index">
                   <span :class="{'Done': item.status == 'Done'} "> 
                       {{ item.name }} 
                    </span>
                    <span class="Status">
                        <span :class="{'StatusDone': item.status == 'Done', 
                            'StatusPending': item.status == 'Pending', 
                            'StatusWIP': item.status == 'WIP'} ">
                        
                                {{item.status}}
                        
                        </span>
                    </span>
                    <button class="Button" @click="editTask(index)" > 
                        Edit
                    </button>
                    <button class="Button" @click="editStatus(index)"> 
                        Status
                    </button>
                    <button class="ButtonRED" @click="remove(index)">
                        Delete
                    </button>
                </li>
            </ul>
        </div>

        <button class='ButtonRED' @click="deleteAll(index)" >
            DELETE ALL 
        </button>

    </div>
    <span class='Counter'>
        there are currently {{items.length}} items in your To Do's
    </span>
    </div>
</template>

<script>
export default {
    
    name: "Test",
    data() {
        return{
            
            items:[],
            item: '',
            editedTask: null,
            defaultStatus: 'To do',
            availableStatus: ['Pending', 'WIP', 'Done'],
            
        }
    },
    methods: {
        
        add(item){
            if (this.item.length != 0) {
                if (this.editedTask === null){
                    this.items.push(
                        {name: this.item,
                        status: "Pending"
                        });
                }else{
                    this.items[this.editedTask].name = this.item;
                    this.editedTask = null;
                    console.log("checking")
               }
            }
               this.item = '';
        },
        remove(index){
            this.items.splice(index,1);
        },
         editTask(index) {
            this.item = this.items[index].name;
            this.editedTask = index;
            
        },
        editStatus(index){
            let newIndex = this.availableStatus.indexOf(this.items[index].status);
            if(++newIndex > 2) newIndex = 0; 
            
            this.items[index].status =  this.availableStatus[newIndex];
        },  
        deleteAll(index){
            this.items.splice(index)
        }
    },
}
</script>

<style scoped src="..\assets\styles.css">
</style>