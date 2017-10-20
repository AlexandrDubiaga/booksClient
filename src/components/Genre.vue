<template>
  <div v-if="genre" class="genre">
  <p class="title">What id: {{genre.id}}</p>
    <table class="table">
      <caption></caption>
      <tbody>
      <tr>
        <th>Name Genre</th>
      </tr>

      <tr>
      <td>{{genre.name}}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Genre',
  props: ['genre']
}
</script>
<style scoped>
.genre{
  text-align: center;
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