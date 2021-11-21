<template>
  <div class="modal" :class="{'active': open}">>
    <div class="overlay" @click="$emit('close')"></div>
    <div class="modal-card">
        <p>{{ year }}년 {{ month }}월 {{ clickDay }}일</p>
        <input type="text" v-model="todolist">
        <button  @click="save">등록</button>
        <!-- <ul>
            <li v-for="(todolist, index) in todolists" :key="todolist">
                {{todolist}}
            </li>
        </ul> -->
      <!-- <slot /> -->
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
    data: function() {
        return {
            todolist: '',
            // todolists:[]
        }
    },
    props: ['open', 'year', 'month', 'clickDay'],
    methods: {
        save: function() {
            var url = 'https://jsonplaceholder.typicode.com/users';
            const data = {
          year: this.year,
          month: this.month,
          day: this.clickDay,
          message: this.todolist,
        };

       axios.post(url, data)
       .then(function(response){
           console.log(response);
      })
      .catch(function(error){
        console.log(error);
        alert('등록 불가');
      });
    //   this.todolists.push({
    //       message: this.todolist
    //   })
    },

  },
};
</script>

<style>
/* Modal */
.modal,
.overlay {
  width: 100%;
  height: 100%;
  position: fixed;
  left: 0;
  top: 0;
}
.overlay {
  opacity: 0.5;
  background-color: black;
}
.modal-card {
  position: relative;
  max-width: 80%;
  margin: auto;
  margin-top: 30px;
  padding: 20px;
  background-color: white;
  min-height: 500px;
  z-index: 10;
  opacity: 1;
}
</style>