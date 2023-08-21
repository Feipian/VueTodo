<template>
    <div class="task">
        <h3>{{ task.title }}</h3>
        <div class="icons" >
            <div class="delete" @click="taskStore.deleteTask(task.id)">
                <span class="material-symbols-outlined" >
                delete_forever
                </span>
                
            </div>
            
            <div class="favorite" >
                <span class="material-symbols-outlined" :class="{active : task.isFav}" @click="taskStore.toggleFav(task.id)">
                    favorite
                </span>
            </div>
            
            
            
            
        </div>

    </div>
</template>

<script>
import { useTaskStore } from '../../stores/TaskStore'
    export default {
        props:['task'],
        setup(){
            const taskStore = useTaskStore()

            return { taskStore }
        }
    }
</script>