<template>
   
    <div class="regForm">
      <p class="alert-danger">{{errorMsg}}</p>
      <div v-if="success !== 'success'">
        <fieldset>
            <div id="legend">
            <legend class="title">РЕГИСТРАЦИЯ</legend>
            </div>
            <div class="control-group">
            <!-- firstName -->
            <label class="control-label"  for="firstName">Имя</label>
            <div class="controls">
                <input v-model="firstName" type="text" id="firstName" name="firstName" placeholder="" >
            </div>
            </div>
            <div class="control-group">
            <!-- lastName -->
            <label class="control-label"  for="lastName">Фамилия</label>
            <div class="controls">
                <input v-model="lastName" type="text" id="lastName" name="lastName" placeholder="" >
            </div>
            </div>
            <div class="control-group">
            <!-- login -->
            <label class="control-label"  for="login">Логин</label>
            <div class="controls">
                <input v-model="login" type="text" id="login" name="login" placeholder="" >
            </div>
            </div>
        
            <div class="control-group">
            <!-- Password-->
            <label class="control-label" for="password">Пароль</label>
            <div class="controls">
                <input v-model="pass" type="password" id="password" name="password" placeholder="" >
            </div>
            </div>
        
            <div class="control-group">
            <!-- Password -->
            <label class="control-label"  for="password_confirm">Пароль (подтверждение)</label>
            <div class="controls">
                <input v-model="passConf" type="password" id="password_confirm" name="password_confirm" placeholder="" >
            </div>
            </div>
        
            <div class="control-group">
            <!-- Button -->
            <div class="controls">
                <button v-on:click="registration()" class="btn  btn-success">Register</button>
                <router-link to='/'><button class="btn btn-success">Back</button></router-link>
            </div>
            </div>
        </fieldset>
    </div>
    <div v-else class="success">
      <h2>Thank you <strong>{{fullName}}</strong>, </h2>
      <router-link class="link" to='/'> to Main page </router-link>
    </div>
    </div>
 
</template>

<script>
import axios from 'axios'
export default {
  name: 'registrationForm',
  data () {
    return {
      firstName: '',
      lastName: '',
      login: '',
      pass: '',
      passConf: '',
      config: {
        headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
            }
      },
      success: '',
      errorMsg: ''
    }
  },
  methods: {
      registration: function () {
          var self = this
          self.errorMsg = ''
          if (self.firstName && self.lastName && self.login && self.pass && self.passConf)
          {
              if (self.firstName.length <= 2)
              {
                  self.errorMsg = 'First name should be at least 3 characters'
                  return false
              }
              if (self.lastName.length <= 2)
              {
                  self.errorMsg = 'Last name should be at least 3 characters'
                  return false
              }
              if (self.pass.length <= 3)
              {
                  self.errorMsg = 'Password should be at least 4 characters'
                  return false
              }
              if(self.pass != self.passConf)
              {
                  self.errorMsg = 'Password fields do not match'
                  return false
              }
            
                var data = new URLSearchParams();
                data.append('first_name', self.firstName)
                data.append('last_name', self.lastName)
                data.append('login', self.login);
                data.append('pass', self.pass);
                axios.post('http://bookShop/user2/bookShop/client/api/users/', data, self.config)
                    .then(function (response) {
                    if (response.data === 1)
                    {
                        self.success = 'success'
                    }
                    else
                    {
                        self.errorMsg = response.data
                    }
                })
                    .catch(function (error) {
                    console.log(error);
                });
          }
          else{
              self.errorMsg =  'Enter data in all fields!'
          }
      },
      checkUser: function(){
          var self = this
          if (localStorage['user']){
              self.$router.push('/')
          }
      }
  },
  computed: {
    fullName(){
      return this.firstName + ' ' + this.lastName
    }
  },
  created(){
      this.checkUser()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.regForm{
background-color:#32CD32;
padding-left:400px;
padding-bottom:400px;
}
.x
{
    position:absolute;
    top:10px;
}

</style>
