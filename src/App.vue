<template>
  <div id="app">
    <div  v-show="isShow">
      <img alt="Vue logo" src="./assets/abc.png">
      <h1>Welcome tây vương mẫu</h1>
    </div>
    <hr/>
    <button @click="isShow = !isShow">
      <span v-show="isShow">Show</span>
      <span v-show="! isShow">Hide</span>
    </button>
    <hr/>
    <input type="text" :disabled="inputDisable"/>
    <button @click="inputDisable = ! inputDisable">Lock/Unlock</button>
    <hr>
    <div v-for="(club, index) in listClub" :key="index">
      <span :class="{color : isColor}">{{ club.name }} : {{ club.country }}</span>
    </div>
    <button @click="isColor = ! isColor">Click Show Color</button>
    <hr>
    <button class="box" @click="numbers" @click.prevent="number = 100" >{{ number }}</button>
    <hr>
    <input type="text" v-model="newTask">
    <button @click="addTask()">Created</button>
    <div v-for="(task, index) in tasks" :key="index">
        {{ task }}
    </div>
    <hr>
    <input type="text" v-model="value">
    {{ value }}
    <button @click="clickChange()">Click here!</button>
    <hr>
    <Props1 v-for="(club, index) in listClub" :key="index" :clubProps="club" />
    <hr>
    <Props2 v-for="(club, index) in listClub" :key="index" :PropsSecond="club" />
    <hr>
    <div>{{ toDay | formatDate }}</div>
    <hr>
    <User :load="dataUser"/>
    <hr>
    <Test />
    <hr>
    

  </div>
</template>

<script>
  import Test from './components/Test.vue'
  import Props1 from './components/Props1.vue'
  import Props2 from './components/Props2.vue'
  import User from './components/User.vue'
  import {HTTP} from './common/http-common';
  import axios from 'axios'
  export default {
    name : 'App',
    components : {
      Test, Props1, Props2, User
    },
    data() {
      return {
        isShow : true,
        inputDisable : true,
        listClub : [
          {name : 'Manchester United', country : 'England'},
          {name : 'Real Madrid', country : 'Spain'},
          {name : 'AC Milan', country : 'Italy'},
        ],
        isColor : true,
        number :0,
        newTask :'',
        tasks : [],
        value:'',
        toDay: new Date().toDateString(),
        dataUser: [],
        errors: []
      }
    },
    methods:{
      numbers(){
        this.number +=10;
      },
      addTask(){
        this.tasks.push(this.newTask);
      },
      clickChange(){
        this.value='Value is changed !'
      }
    },
    watch: {
      value(){
        console.log('Value da thay doi');
      }
    },
    filters: {
      formatDate(param){
        if(!param) return '';
        const date = new Date(param);
        const day = date.getDate();
        const month = date.getMonth() +1;
        const year = date.getFullYear();
        return `${day}/${month}/${year}`;
      }
    },
    //call api
    created(){
      // axios.get(`http://localhost:3000/posts`,{
      //   params: {
      //     title: 'Java'
      //   }
      // })
      HTTP.get(`posts`)
      .then(response =>{
        this.dataUser = response.data
      })
      .catch(e =>{
        this.errors.push(e)
      })
    }


  }
</script>

<style>
.color{
  color: red;
}
.box{
  border: 1px solid green;
  border-radius: 3px;
  padding: 3px 5px;
  margin: 3px 5px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

































