<template>
  <div v-if="author" class="author">
  <p class="title">What id: {{author.id}}</p>
    <table class="table">
      <caption></caption>
      <tbody>
      <tr>
        <th>Name Author</th>
      </tr>

      <tr>
      <td>{{author.name}}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Author',
  props: ['author']
}
</script>
<style scoped>
.author{
  text-align: center;
  margin-top:-500px;
}
.table{
  width: 500px;
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