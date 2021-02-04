<template>
    <ul>
        <li>
        {{ task.title }}
        <div class="actions float-right">
        <a href="javascript:void(0)" @click="completeTask" class="mx-2"><i class="fas fa-check text-success"></i></a>
        <a href="javascript:void(0)" @click="removeTask" class="mx-2"><i class="fas fa-times text-danger"></i></a>
        </div>              
    </li>
    <hr>
    </ul>    
</template>

<script>
export default {
    data(){
        return {
        }
    },
    props: {
        task: {
            type: Object,
            required: true
        }
    },
    methods: {
        completeTask(){
            this.$emit('completeTask', this.task)
        },
        removeTask(){
            this.$emit('removeTask', this.removed)
        },
    }
}
</script>

