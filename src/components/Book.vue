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
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Book',
  props: ['book']
}
</script>
<style scoped>
.book{
  text-align: center;
  margin-top:-2450px;
  margin-right:-500px;
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