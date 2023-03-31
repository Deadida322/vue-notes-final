<template>
  <div id="app">
    <div class="container">
      <KForm @onNoteSave="saveNote" :editStatus="editStatus" :editableNote="editableNote" @onNoteAdd="addNote" />
      <template v-if="notes.length">
        <transition-group name="list">
          <KNote :key="index" :class="{ 'editable-note': index === currentIndex }" @onNoteEdit="editNote(index)"
            @onNoteDelete="deleteNote(index)" class="mt-4 note" v-for="(note, index) in notes" :note="note" />
        </transition-group>
      </template>
      <div v-else class="alert alert-warning mt-4" role="alert">
        Добавьте хотя бы одну заметку
      </div>

    </div>
  </div>
</template>

<script>
import Swal from "sweetalert2";
import KForm from "./components/KForm.vue"
import KNote from "./components/KNote.vue";
export default {
  name: 'App',
  components: {
    KForm,
    KNote
  },
  created() {
    const notes = JSON.parse(localStorage.getItem("notes"))
    if (notes) {
      this.notes = notes
    }
  },
  data() {
    return {
      editStatus: false,
      editableNote: {},
      currentIndex: false,
      notes: [
        {
          title: "aaa1",
          description: "bbb"
        }, {
          title: "aaa2",
          description: "bbb2"
        }
      ]
    }
  },
  methods: {
    addNote(note) {
      this.notes.push(note)
    },
    deleteNote(index) {
      this.notes.splice(index, 1)
      Swal.fire(
        'Отлично!',
        'Заметка была успешно удалена',
        'success'
      )
    },
    editNote(index) {
      this.editStatus = true
      this.currentIndex = index
      this.editableNote = this.notes[index]
    },
    saveNote(note) {
      console.log(note)
      this.notes.splice(this.currentIndex, 1, note)
      this.editStatus = false
      this.editableNote = {}
      this.currentIndex = false

      Swal.fire(
        'Отлично!',
        'Заметка была успешно изменена',
        'success'
      )
    }
  },
  watch: {
    notes(val) {
      localStorage.setItem('notes', JSON.stringify(val))
    }
  }
}
</script>

<style>
.list-enter-active,
.list-leave-active {
  transition: all 1s;
}

.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


.editable-note {
  opacity: .8;
  transform: translateX(+10px);
  border: 2px solid grey;
}

.note {
  transition: all .2s ease-in
}
</style>
