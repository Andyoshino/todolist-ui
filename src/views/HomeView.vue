<template>
  <div class="container mx-auto my-10 flex h-[800px] w-[960px] gap-3">

      <div class="w-1/3">
          <div class="h-2/5 rounded-2xl overflow-hidden shadow-xl bg-slate-50">
              <div class="bg-gradient-to-b from-red-500 to-pink-500 text-white h-8 py-1 text-center">
                  <h1>Input Task</h1>
              </div>

              <div class="w-full p-6 flex">
                  <FormTodo class="m-auto mt-4"></FormTodo>
              </div>


          </div>

          <div class="h-3/5 rounded-2xl overflow-hidden shadow-xl bg-slate-50 mt-2">
              <div class="bg-gradient-to-b from-blue-500 to-sky-500 text-white h-8 py-1 text-center">
                  <h1>Query Setting</h1>
              </div>

              <div class="w-full p-6 flex">
                  <QuerySetting class="m-auto mt-4" :cur-page-prop="curPage" :page-size-prop="pageSize" @clicked="executeQuery"></QuerySetting>
              </div>

          </div>

      </div>

      <div class="w-2/3 h-full bg-gradient-to-br from-sky-600 to-blue-400 rounded-tr-2xl rounded-bl-2xl shadow-xl p-4 overflow-y-scroll">
          <div class="container w-full">

              <div class="bg-slate-50 mx-auto w-48 p-2 rounded-2xl">
                <h1 class="text-center">To do List!</h1>
              </div>

              <div class="container w-full p-8">
                  <TodoComponent v-for="(todos) in listTodos" v-bind:key="todos.id" :todo="todos"></TodoComponent>
              </div>



          </div>
      </div>

  </div>
</template>

<script>
import FormTodo from "@/components/FormTodo";
import QuerySetting from "@/components/QuerySetting";
import TodoComponent from "@/components/TodoComponent";
import axios from "axios";

export default {
    name: 'HomeView',
    components: {
      FormTodo, QuerySetting, TodoComponent
    },
    methods: {
        refreshPage() {
            axios({
                method: "get",
                url: "/api/todos?curPage=" + this.curPage + "&pageSize=" + this.pageSize + "&sort=" + this.sort + "&filter=" + this.filter
            })
                .then((res) => {
                    this.listTodos = res.data.listTodo;
                    this.curPage = res.data.curPage;
                    this.pageSize = res.data.pageSize;
                    this.lastPage = res.data.lastPage;
                    this.tempNumber = (this.curPage-1)*this.pageSize;
                    this.displayPage = this.curPage;
                })
                .catch((err) => console.error(err));
        },
        executeQuery(req) {
            console.log(req);
            this.pageSize = req.pageSize;
            this.curPage = req.curPage;
            this.filter = req.filter;
            this.refreshPage();
        }
    },
    data() {
        return {
            listTodos : [],
            curPage : 0,
            lastPage : 0,
            pageSize : 0,
            sort : '',
            task : '',
            schedule : '',
            badRequest : '',
            filter : '',
            tempNumber : 0,
            displayPage : 0
        }
    },
    mounted() {
        axios({
            method: "get",
            url: "/api/todos"
        })
            .then((res) => {
                this.listTodos = res.data.listTodo;
                this.curPage = res.data.curPage;
                this.pageSize = res.data.pageSize;
                this.lastPage = res.data.lastPage;
                this.tempNumber = (this.curPage-1)*this.pageSize;
                this.displayPage = this.curPage;
            })
            .catch((err) => console.error(err));
    }
}
</script>

<style>
::-webkit-scrollbar {
    display: none;
}
</style>
