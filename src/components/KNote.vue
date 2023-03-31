<template>
    <div class="card">
        <div class="card-body d-flex flex-column align-items-start">
            <h5 class="card-title">{{ note.title }}</h5>
            <p class="card-text">{{ note.description }}</p>
            <div class="d-flex w-100 flex-row-reverse">
                <button @click="$emit('onNoteEdit')" class="btn m-1 btn-warning">Редактировать</button>
                <button @click="$emit('onNoteDelete')" class="btn  m-1 btn-danger">Удалить</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        note: {

        }
    },

}

</script>