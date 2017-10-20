<template>
  <div v-if="book" class="book">
  <p class="title">What id: {{book.id}}</p>
    <table class="table">
      <caption></caption>
      <tbody>
      <tr>
        <th>Name Book</th>
        <th>Price</th>
        <th>Description</th>
        <th>Discount</th>
        <th>Active</th>
        <th>Img</th>
        <th>Author</th>
        <th>Genre </th>
          <th>Details </th>
      </tr>
      <tr>
      <td>{{book.title}}</td>
      <td>{{book.price}}</td>
      <td>{{book.description}}</td>
      <td>{{book.discount}}</td>
      <td>{{book.active}}</td>
       <td>{{book.img}}</td>
       <td>{{book.a_name}}</td>
       <td>{{book.g_name}}</td>
       <td> <div class="btnPreOr" v-if="checkUser > 0">
                <router-link :to="{name: 'order', params: { obj: book }}"><button class="btn btn-primary">Details</button></router-link>
            </div></td>
      </tr>
      </tbody>
     
    </table>
  </div>
 
</template>

<script>
import axios from 'axios'
 import Order from './Order'
export default {
  name: 'Book',
  props: ['book'],
   data(){
            return {
                user: {
        id: '',
        hash: '',
        firstName: '',
      },
                checkUser: 0,
                config: {
                    headers: {
                        'Content-Type': 'application/x-www-form-urlencoded'
                    }
                }
            }
        },
        methods: {
     getCheck: function(){
                var self = this
                self.user = JSON.parse(localStorage['user'])
                if (self.user.id && self.user.hash)
                {
                 
                    self.checkUser = 1
                     
                }
                else{
                    self.checkUser = 0
                }
            },
  },
  created(){
            this.getCheck()
        }
          
}
</script>
<style scoped>
.book{
  text-align: center;
}
.table{
  width: 700px;
  margin: auto;
  border: 2px dashed red;
}
.table tr th{
  text-align: center;
   border: 2px solod pink;
}
.title{
  color: blue;
  font-size: 18px;
}
</style>