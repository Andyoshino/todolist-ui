<template>
    <div class="">
        <form class="todo-form" @submit.prevent="handleSubmit">

            <h5>Task</h5>
            <input type="text" class="my-2 focus:outline-pink-400 w-full">

            <h5>Schedule</h5>
            <input type="date" class="my-2 focus:outline-pink-400 w-full">

            <button class="mt-4 block mx-auto h-8 text-white rounded-md px-4 bg-gradient-to-tl from-red-500 to-pink-500">submit</button>

        </form>
    </div>
</template>

<script>
export default {
    name: 'FormTodo',
    props: {
        editData: {
            type: Object,
            default: null
        }
    },
    data () {
        return {
            text: this.editData ? this.editData.text : ''
        }
    }
}
</script>