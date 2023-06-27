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
    <div>
     <input type="text" :disabled="inputDisable"/>
    <button @click="inputDisable = ! inputDisable">Lock/Unlock</button> 
    </div>
    <hr>
    <div v-for="(club, index) in listClub" :key="index">
      <span :class="{color : isColor}">{{ club.name }} : {{ club.country }}</span>
    </div>
    <div>
     <button @click="isColor = ! isColor">Click Show Color</button> 
    </div>
    <hr>
    <div>
    <button class="box" @click="numbers" @click.prevent="number = 100" >{{ number }}</button>  
    </div>
    <hr>
    <div>
      <input type="text" v-model="newTask">
    <button @click="addTask()">Created</button>
    <div v-for="(task, index) in tasks" :key="index">
        {{ task }}
    </div>
    </div>
    <hr>
    <div>
    <input type="text" v-model="value">
    {{ value }}
    <button @click="clickChange()">Click here!</button>  
    </div>
    <hr>
    <div>
    <Props1 v-for="(club, index) in listClub" :key="index" :clubProps="club" />  
    </div>
    <hr>
    <div>
    <Props2 v-for="(club, index) in listClub" :key="index" :PropsSecond="club" />  
    </div>
    <hr>
    <div>{{ toDay | formatDate }}</div>
    <hr>
    <div>
    <User :load="dataUser"/>  
    </div>
    <hr>
    <div>
    <Test />  
    </div>
    <hr>
        <div><h1 style="text-align: center;">Vue Resource</h1></div>
        <div>
          <div>
            <input type="text" v-model="account.username" placeholder="Nhập tên tài khoản"/>
          </div>
          <div>
            <input type="text" v-model="account.email" placeholder="Nhập địa chỉ mail"/>
          </div>
          <div>
            <button @click="submit">Submit</button>
          </div> 
        </div>
        <div>
          <div>User name : {{ account.username }} </div>
          <div>Email : {{ account.email }}</div>
        </div>
    <hr>
        <div>
          <button @click="getAllAccounts">Get All Data</button>
          <table class="style table" v-if="accounts.length > 0">
            <tr class="style">
              <th class="style">USERNAME</th>
              <th class="style">EMAIL</th>
            </tr>
            <tr class="style" v-for="(acc, index) in accounts" :key="index">
              <td class="style">{{ acc.username }}</td>
              <td class="style">{{ acc.email }}</td>
            </tr>
          </table>
        </div>











  </div>
</template>

<script>
  import Test from './components/Test.vue'
  import Props1 from './components/Props1.vue'
  import Props2 from './components/Props2.vue'
  import User from './components/User.vue'
  import {HTTP} from './common/http-common';
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
        errors: [],
        account: {
          username: '',
          email: ''
        },
        accounts :[]
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
      },
      submit(){
        // return console.log(this.account);
        this.$http.post('https://examble-vue-default-rtdb.firebaseio.com/data.json', this.account)
          .then(response => {
            console.log(response);
          }, error => {
            console.log(error);
          })
      },
      getAllAccounts(){
        this.$http.get('https://examble-vue-default-rtdb.firebaseio.com/data.json')
          .then(response => {                   //đoạn này nhớ tới promies 2 lần then
            console.log(response.json());              //lần then thứ nhất return ra cái gì
            return response.json();               //lần then thứ 2 sẽ nhất được cái đó 
          })                                    // response.json = data
          .then(newdata =>{
            const newArray = []
            console.log(newdata);
            for(let x in newdata){
              newArray.push(newdata[x]);
            }
            console.log(newArray);
            this.accounts = newArray;
          })   
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

































