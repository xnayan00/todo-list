<template>
    <div class="col-md-4">
        <div class="mb-4">
            <h3>Nova Tarefa</h3>
            <div class="custom-hr"></div>
        </div>
        <div class="new-task">
            <input v-model="title" class="form-control mb-3" type="text" placeholder="Título da tarefa">
            <a href="javascript:void(0)" class="new-task-btn" @click="addTask">Adicionar Tarefa</a>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            title: ''
        }
    },
    methods: {
        addTask(){
           this.$emit('addTask', this.title)
           this.title = ''
        }
    }
}
</script>