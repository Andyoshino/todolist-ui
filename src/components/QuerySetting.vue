<template>
    <div class="">
        <form class="todo-form" @submit.prevent="sendToParent">

            <h5>Filter Task</h5>
            <input type="text" class="px-2 my-4 focus:outline-sky-400 w-full" placeholder="masukkan filter..." v-model="filter">

            <h5>Current Page</h5>
            <input type="number" class="px-2 my-4 focus:outline-sky-400 w-full" v-model="curPage">

            <h5>Page Size</h5>
            <input type="number" class="px-2 my-4 focus:outline-sky-400 w-full" v-model="pageSize">


            <button class="mt-6 block mx-auto h-8 text-white rounded-md px-4 bg-gradient-to-tl from-blue-500 to-sky-500">execute</button>

        </form>
    </div>
</template>

<script>
export default {
    name: 'QuerySetting',
    props: ['curPageProp', 'pageSizeProp'],
    data () {
        return {
            filter: '',
            curPage: this.curPageProp == 0 ? 1 : this.curPageProp,
            pageSize: this.pageSizeProp == 0 ? 1 : this.pageSizeProp
        }
    },
    methods: {
        sendToParent() {
            this.$emit('clicked', {
                filter : this.filter,
                curPage : this.curPage,
                pageSize : this.pageSize
            })
        }
    }
}
</script>