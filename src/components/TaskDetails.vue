<template>
    <div class="task">
        <h3>{{ task.title }}</h3>
        <div class="icons">
            <i class="material-icons" @click="handleDelete" >delete</i>
            <i class="material-icons" :class="{isFav: task.isFav}" @click="handleFav">favorite</i>
        </div>
    </div>
</template>

<script>
import { useTaskStore } from '../stores/TaskStore';

    export default {
        props: {
            task: {
                type: Object,
                required: true
            }
        },
        setup(props){
            const taskStore = useTaskStore();
            const handleDelete = () => {
                taskStore.deleteTask(props.task.id)
            }

            const handleFav = () => {
                taskStore.toggleFav(props.task.id)
            }

            return {handleDelete,handleFav}
        }
    }
</script>