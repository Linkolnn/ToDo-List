<script setup>
import { ref, computed } from "vue"

const _todo_list = ref([]),
      _todo_text = ref(""),
      _pending = computed(() => {
            return _todo_list.value.filter(item => !item.checked)
      }),
      _done = computed(() => {
            return _todo_list.value.filter(item => item.checked)
      });

      function clearToDo () {
        _todo_text.value = "";
      } 

      function addToDo () {
        if (_todo_text.value && _todo_list.value !== "") {
            _todo_list.value.push({
                id: new Date().valueOf,
                text: _todo_text.value,
                checked: false
            });
            clearToDo()
        }
      }

      function deleteToDo (id) {
        _todo_list.value.splice(id, 1)
      }

</script>

<template>
    <div class="todo_section section">
        <div class="todo_container shd_grd_r">
            <h1 class="todo_title">
                <i class="fa-solid fa-clipboard-list"></i>
                To-Do List
            </h1>
            <div class="todo_inp_block">
                <div class="inp_block">
                    <input class="inp todo_inp" 
                        type="text" 
                        autofocus
                        v-model="_todo_text"
                        @keyup.enter="addToDo()"
                        placeholder="Написать заметку">
                    <button class="btn todo_inp_btn" @click="clearToDo()">
                        <i class="fa-solid fa-times"></i>
                    </button>
                </div>
                <div class="todo_inp_btn_block shd_grd_r">
                    <button class="btn todo_btn" @click="addToDo()">
                        <i class="fa-solid fa-plus"></i>
                    </button>
                </div>
            </div>
            <div class="todo_lists">
                <div class="todo_pending_block todo_block_list">
                    <div class="todo_pending">Не выполнено {{ _pending.length }}</div>   
                    <div class="todo_pending_list todo_list" v-for="todo in _pending" :key="todo.id">
                        <label class="todo_item">
                            <input class="todo_checkbox" type="checkbox" v-model="todo.checked">
                            <span class="todo_text">{{ todo.text }}</span>
                        </label>
                    </div>
                    <div class="todo_tasks" v-show="_pending.length == 0">No tasks</div>
                </div>

                <div class="todo_done_block todo_block_list">
                    <div class="todo_done">Выполнено {{ _done.length }}</div>   
                    <div class="todo_done_list todo_list" v-for="todo in _done" :key="todo.id">
                        <label class="todo_item">
                            <input class="todo_checkbox btn" type="checkbox" v-model="todo.checked">
                            <span class="todo_text">{{ todo.text }}</span>
                            <button class="done_btn btn" @click="deleteToDo(todo.id)">delete</button>
                        </label>
                    </div>                 
                    <div class="todo_tasks" v-show="_done.length == 0">No tasks</div>
                </div>
            </div> 
        </div>
    </div>
</template>