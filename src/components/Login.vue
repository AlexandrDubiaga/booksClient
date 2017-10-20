<template>
  <div class="login navbar-form" >
    <div v-if="checkUser == ''">
        <div class="form-group">
            <input v-model="login" type="text" class="form-control" name="username" placeholder="Username">
        </div>
        <div class="form-group">
            <input v-model="pass" type="password" class="form-control" name="password" placeholder="Password">
        </div>
        <button v-on:click="loginFun()" type="submit" class="btn btn-primary">Sign In</button>
        <router-link class="regist" to="/registration">Registration</router-link>
        <p><span class="alert-danger">{{errorMsg}}</span></p>
    </div>
    
    <div v-else class="form-group">
      <p class="hello">Hi , <span>{{user.firstName}}</span>!</p>
      <p class="myOrders"><button v-on:click="myOrders()" type="submit" class="btn btn-primary">User Orders</button></p>
      <p class="myCart"><router-link class="cart" to="/cart"><button type="submit" class="btn btn-primary">User Cart</button></router-link></p>

      <p class="logout"><button v-on:click="logoutFun()" type="submit" class="btn btn-primary">Exit</button></p>

      <p v-if="role == 'admin'" class="admin"><router-link to="/admin"><button type="submit" class="btn btn-danger">Admin</button></router-link></p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'loginForm',
  data () {
    return {
      login: '',
      pass: '',
      checkUser: '',
      errorMsg: '',
      user: {
        id: '',
        hash: '',
        firstName: '',
      },
      role: '',
      config: {
        headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
            }
      },
    }
  }, 
  methods: {
    loginFun: function(){
      var self = this
      self.errorMsg = ''
        if (self.login && self.pass)
        {
          axios.put('http://bookShop/user2/bookShop/client/api/users/', {
            login: self.login,
            pass: self.pass
          }, self.config)
          .then(function (response) {
            if (response.data.id && response.data.hash)
            {
              self.user.id = response.data.id
              self.user.hash = response.data.hash 
              self.user.firstName = response.data.first_name
              self.role = response.data.role
              localStorage['user'] = JSON.stringify(self.user)
              self.checkUserFun()
              self.$parent.getCheck()
              if (self.role == 'admin')
              {
                self.$router.push('/admin')
              }
              return true
            }
            else {
              self.errorMsg = response.data
            }
          })
          .catch(function (error) {
            console.log(error)
          });
        }
        else
        {
          self.errorMsg = 'Enter data in all fields!'
        }
    },
    checkUserFun: function(){
      var self = this
      if (localStorage['user'])
      {    
        self.user = JSON.parse(localStorage['user'])
        axios.get('http://bookShop/user2/bookShop/client/api/users/' + self.user.id)
            .then(function (response) {
                if (self.user.hash === response.data[0].hash)
                {
                      
                    self.checkUser = 1;
                    self.role = response.data[0].role
                    return true
                }
                else
                {
                  self.checkUser = ''
                  delete localStorage['user']
                }

            })
            .catch(function (error) {
              console.log(error)
            });
      }
      else{
        self.checkUser = ''
        return false
      }
    },
    logoutFun: function(){
      var self = this
      delete localStorage['user']
      self.checkUser = ''
      self.pass = ''
      self.$parent.getCheck()
      //self.$parent.setFilterValues('', '')
    },
   // myOrders: function(){
     // var self = this
    //  self.$parent.setMyOrder()
   // }
  },
  created(){
    this.checkUserFun()
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.login{
 
  padding-top: 7px;
  padding-bottom: 8px;
  bottom: 7px;
}
.form-group{
  padding-bottom: 10px;
}
.regist{
  margin-left: 30px;
}
.hello {
  font-weight: bold;
  font-size: 18px;
  color: darkblue;
}
.myCart {
  position: absolute;
  top: 10px;
  left: 260px;
}
.admin{
  position: absolute;
  top: 84px;
  left: 0px;
}
.myOrders
{
   position: absolute;
  top: 10px;
  left: 150px;
}

</style>
