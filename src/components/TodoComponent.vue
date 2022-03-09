<template>
    <div class="w-full h-20 bg-gradient-to-br from-cyan-300 to-sky-500 flex overflow-hidden rounded-l-full hover:scale-110 transition my-8" v-bind:class="{'opacity-50' : isDone }">

        <div class="w-10/12 pl-10 flex flex-wrap p-2 transition" @click="isDone=!isDone">
            <div class="my-auto w-full">
                <div class="bg-white w-fit px-2 rounded-sm shadow-md">{{todo.task}}</div>
                <div class="bg-white w-fit px-2 rounded-sm shadow-md mt-1">{{todo.schedule}}</div>
            </div>


        </div>

        <div class="w-2/12 flex flex-wrap p-2">

            <div class="w-full my-auto bg-white text-center rounded-lg shadow-md hover:bg-slate-700 hover:text-white transition">
                <button>delete</button>
            </div>

            <div class="my-auto bg-white text-center rounded-lg w-full shadow-md hover:bg-slate-700 hover:text-white transition">
                <button>edit</button>
            </div>

        </div>

    </div>
</template>

<script>
export default {
    name: 'TodoComponent',
    props: ['todo'],
    data () {
        return {
            text: this.editData ? this.editData.text : '',
            isDone : false,
            mutableTodo : this.todo
        }
    }
}
</script>