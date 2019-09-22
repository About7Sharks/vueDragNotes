<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <br>
    <input placeholder="Enter text..." v-model="noteText" type="text"><button @click="createNote()">Add Note</button>
    <div>
      <p class="draggable card card-1" v-for='(note,i) in notes' :key='i'>
       {{i+1}}: {{note}}
      </p>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import Draggabilly from 'draggabilly'
export default {
  name: 'home',
  components: {
    // HelloWorld
  },
  data(){
    return{
      noteText:'',
      notes:[]
    }
  },
  methods:{
    createDragEl(){
      var draggableElems = document.querySelectorAll('.draggable');
      // array of Draggabillies
      var draggies = []
      // init Draggabillies
      for ( var i=0; i < draggableElems.length; i++ ) {
        var draggableElem = draggableElems[i];
        var draggie = new Draggabilly( draggableElem, {
          // options...
        });
        draggies.push( draggie );
      }
    },

   createNote(){
      this.notes.push(this.noteText)
        this.$nextTick(()=>{
          this.createDragEl()
        })  
    }
  },
  mounted(){
    this.createDragEl()
      }
}
</script>
<style lang="scss" scoped>
.card {
  background: #fff;
  border-radius: 2px;
  display: inline-block;
  margin: 1rem;
  position: relative;
  padding: 10px;
}
.card-1 {
  box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
  transition: all 0.3s cubic-bezier(.25,.8,.25,1);
}
.card-1:hover {
  box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
}
</style>
