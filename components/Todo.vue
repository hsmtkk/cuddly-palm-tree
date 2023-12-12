<template>
    <form v-on:submit.prevent="addTask">
        <input v-model="newTask" name="newTask" autocomplete="off" />
        <button>Add</button>
    </form>
    <ul>
        <li v-for="(task, index) in tasks" :key="task">{{ task }}<button v-on:click="deleteTask(index)">Delete</button></li>
    </ul>
    <button v-on:click="clearTask">Clear</button>
</template>

<script setup lang="ts">
const tasks: string[] = useCookie("tasks", {
    default: () => ["alpha", "bravo"],
})

const newTask = ref("")

function addTask() {
    console.log(`adding ${newTask}`)
    if (newTask.value.length > 0) {
        tasks.value.push(newTask.value)
    }
    newTask.value = ""
}

function deleteTask(index: number) {
    tasks.value.splice(index, 1)
}

function clearTask() {
    tasks.value = []
}
</script>
