<template>
    <div class="card">
        <div class="card-body">
            <h5 v-if="!editStatus" class="card-title">Добавить заметку</h5>
            <h5 v-else class="card-title">Изменить заметку</h5>
            <div class="card-text">
                <label class="form-label">Название</label>
                <input v-model="note.title" type="text" class="form-control mb-2" />
                <label class="form-label">Описание</label>
                <textarea v-model="note.description" type="text" class="form-control" />
            </div>
        </div>
        <div v-if="!editStatus" @click="onNoteAdd" class="btn btn-primary m-3 mt-0">Добавить</div>
        <div v-else @click="onNoteSave" class="btn btn-primary m-3 mt-0">Сохранить</div>
    </div>
</template>

<script>
import Swal from "sweetalert2"
export default {
    props: {
        editStatus: false,
        editableNote: {}
    },
    data() {
        return {
            note: {
                title: "",
                description: ""
            }
        }
    },
    methods: {
        onNoteAdd() {
            if (this.note.title) {
                this.$emit("onNoteAdd", { ...this.note })
                this.note = {}
            } else {
                Swal.fire(
                    'Ошибка',
                    'Укажите название заметки',
                    'error'
                )
            }
        },
        onNoteSave() {
            if (this.note.title) {
                this.$emit("onNoteSave", { ...this.note })
                this.note = {}
            } else {
                Swal.fire(
                    'Ошибка',
                    'Укажите название заметки',
                    'error'
                )
            }
        }
    },
    watch: {
        editableNote(val) {
            if (val) {
                this.note = { ...this.editableNote }
            }
        }
    }
}
</script>