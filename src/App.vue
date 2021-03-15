<template>
  <div id="app">
    <h1>Vue.js Markdown Notes!</h1>
    <button id="btn" @click="createNote">Add New Note</button>
    
    <ul id="listNotes">
      <li v-for="note in notes" :key="note.date"><Notas :note="note" @saveMe="saveNotes" @deleteMe="deleteNote($event)"/></li>
    </ul>
  </div>
</template>

<script>
import Notas from './components/Notas';
export default {
  name: 'App',
  data(){
    return{
      notes: [
        {
          date: "Thu Feb 25 2021 at 19:40:10",
          message: "# Hello World!"
        }
      ]
    }
  },
  components: {
    Notas,
  },
  mounted(){
    if(localStorage.getItem('notes')){
      try {
        this.notes = JSON.parse(localStorage.getItem('notes'));
      } catch(e) {
        localStorage.removeItem('notes');
      }
    }
  },
  methods: {
    saveNotes: function(){
      const parsed = JSON.stringify(this.notes);
      localStorage.setItem('notes', parsed);
    },
    createNote: function(){
      let day = new Date();
      let dateCreated = day.toDateString() + ' at '+ day.toLocaleTimeString();
      let convert = String(dateCreated);
      this.notes.push({date: convert});
      this.saveNotes();
    },
    deleteNote: function($event) {
      let id = $event.idNote;
      let newNotes = this.notes.filter(notes => notes.date != id);
      this.notes = newNotes;
      this.saveNotes();
    }
  }
}
</script>

<style>

  *{padding: 0; margin: 0;}
  body{background: #141a20;}

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #fff;
    padding: 30px 0;
    display: flex;
    flex-flow: column;
    align-items: center;
  }
  ul {list-style: none; display: flex; flex-flow: column-reverse;}
  li {margin: 15px 0 20px 0;}

  #btn {
    border: 1px solid #111;
    width: 150px;
    height: 40px;
    font-size: 11pt;
    color: #fff;
    cursor: pointer;
    margin: 35px 0;
    background: #333;
    outline: none;
  }
  #btn:hover {
    background: #222;
    color: #ddd;
  }
</style>
