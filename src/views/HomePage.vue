<template>
  <div class="container">
    <div>
      <p class="section2">click to show yearly tasks</p>
    </div>
    <div class="">
      <div class="button-group">
        <button class="title2" @click="removeAllTasks">remove all tasks</button>
        <button class="title2" @click="markAllDone">Mark all Done</button>
      </div>
      <ul>
        <li v-for="todo in titleTasks" :key="todo.id">
          <div>
            <input type="checkbox" @click="toggleDone(todo)" />
            <h3 :class="{done : todo.done}">{{todo.content}}</h3>
            <h3 :class="{done : todo.done}">{{todo.date}}</h3>
            <h3 :class="{done : todo.done}">{{todo.category}}</h3>
            <button class="delete" @click="confirmDelete">
              <img src="../assets/img/eraser-64.png">
            </button>
            <button class="edit">
              <img src="../assets/img/pencil-96.png">
            </button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 100%;
  display: flex;
  justify-content: space-between;
}

.delete {
  margin-left: 20px;
  cursor: pointer;
}

.edit {
  margin-left: 20px;
  cursor: pointer;
}

.edit img {
  width: 36px;
  height: auto;
}

.delete img {
  width: 36px;
  height: auto;
}

.button-group {
  display: flex;
  justify-content: end;
}
</style>

<script lang="ts" >
import { onMounted, ref } from 'vue'
import type { Ref } from 'vue'
// import ConfirmDelete from '@/components/DeleteModal.vue'

export default {
  setup () {
    interface ItitleTasks {
      id: number,
      done: boolean,
      content: string,
      date: Date,
      category:string,
      // tasks: {
      //   id: number,
      //   done: boolean,
      //   content: string,
      //   data: Date
      // }
      // categories: {
      //   id: number,
      //   title: string,
      // }
    }

    const titleTasks: Ref<ItitleTasks[]> = ref([])
    // const titleTasks = ref([])
    const url = 'http://localhost:3000/tasks'

    const fetchData = () => {
      return fetch('http://localhost:3000/tasks', {
        method: 'GET',
        headers: {
          'content-type': 'application/json'
        }
      }).then(res => { return res.json() })
        .then(json => { titleTasks.value = json })
    }

    onMounted(() => {
      fetchData()
    })

    // to done the task
    function toggleDone (todo: any) {
      todo.done = !todo.done
    }
    // remove just delete it here but keep exist it,delete means delete it completely
    function deleteTask (id: any) {
      const index = titleTasks.value.findIndex(x => x.id === id)
      titleTasks.value.splice(index, 1)
      deleteData(url, id)
    }

    function markAllDone () {
      titleTasks.value.forEach((todo) => {
        todo.done = true
      })
    }

    function removeAllTasks () {
      // titleTasks.value = [];
      titleTasks.value.length = 0
    }
    const deleteData = async (url = '', id: number) => {
      const response = await fetch(url + '/' + id, {
        method: 'DELETE',
        mode: 'cors',
        cache: 'no-cache',
        credentials: 'same-origin',
        headers: {
          'Content-Type': 'application/json'
        },
        redirect: 'follow',
        referrerPolicy: 'no-referrer'
        // body: JSON.stringify(data)
      })
      return response.json()
    }

    // const confirmDelete = () => {
    //     // model opens
    //     // deleteTask(todo.id)
    // }
    return {
      titleTasks,
      toggleDone,
      deleteTask,
      markAllDone,
      removeAllTasks
      // confirmDelete
    }
  }
}
</script>
