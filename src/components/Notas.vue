<template>
    <div class="notas">
        <span >Note Created in {{ note.date }}</span>
        <i class="far fa-save" title="Save" @click="emitSave"></i>
        <i class="far fa-trash-alt" title="Delete" @click="emitDelete"></i>
        <textarea spellcheck="false" placeholder="Type your note here!" v-model="note.message"></textarea>
    </div>
</template>

<script>
export default {
    name: 'Notas',
    data() {
        return{
        }
    },
    props: {
        note: Object
    },
    methods: {
        emitSave: function() {
           this.$emit("saveMe");
           alert("Saved ✔");
        },
        emitDelete: function() {
           this.$emit("deleteMe", {idNote: this.note.date, component: this});
        }
    }
}
</script>

<style scoped>
    .notas {
        width: 60vw;
        height: 80vh;
        text-align: left;
        padding: 5px;
        border-radius: 5px;
        background: #333;
    }

    .far {font-size: 20px; cursor: pointer; margin: 0 5px;}
    .fa-save:hover{color: #20af3f;}
    .fa-edit:hover{color: #fcff3b;}
    .fa-trash-alt:hover{color: #ff2a2a;}

    textarea {
        width: calc(100% - 55px);
        height: calc(100% - 80px);
        color: #fff;
        font-size: 13pt;
        resize: none;
        padding: 25px;
        background: #222;
        outline: none;
    }
</style>