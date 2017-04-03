<template>
  <div id="app">
    <b style="margin-left:25px"> Users List</b><br>
    <template v-for="(user,index) in userList">

      {{++index}}-> {{user.name}}<br>

    </template>
    <hr>
    <div>
      <input type="text" placeholder="User Name" v-model="userName" @keypress.enter="postData" />
      <input type="submit" value="Register" @click="postData" />
    </div>
  </div>
</template>


<script>

    export default {
        name: 'app',
        data () {
            return {
                ajaxRequest:false,
                userList:[],
                userName:''
            }
        },

        methods:{
            getData(){

                this.$http.get('http://jsonplaceholder.typicode.com/users')
                    .then((res)=>res.json())
                    .then(res=>{
                        this.userList= res;
                    });

            },

            postData(){

                let body = {"AdSoyad":this.userName,Id:0};
                body = JSON.stringify(body);
                console.log(body);
                this.$http.post('http://localhost:47523/api/Values/Register', {AdSoyad:this.userName}, function(response) {
                    console.log(response);
                });
            }
        },
        created(){
            this.getData();

        }
    }
</script>

<style lang="scss">
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;

    color: #2c3e50;

  }

  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
</style>
