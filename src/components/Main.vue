<template>

  <div class="main">
  
  <div class="row">
      <div class="col-md-12">
        <loginForm></loginForm>
      </div>
    <div class="col-md-3 ">
    <p class="alert-danger">{{errors}}</p>
      <ul class="nav left-menu">
        <li class="nav-header glyphicon glyphicon-list-alt"> Books</li>
          <li v-for="book in books"> <a href="#" @click=" getBookById(book.id)">{{book.title}}</a></li>
        <li class="nav-header glyphicon glyphicon-book"> Genre </li>
          <li v-for="genre in genres"><a href="#" @click=" getGenresById(genre.id)">{{genre.name}}</a></li>
        <li class="nav-header glyphicon glyphicon-user"> Author</li>
          <li v-for="author in authors"><a href="#" @click=" getAuthorById(author.id)">{{author.name}}</a></li> 
      </ul>
    </div>
    <div v-if="success !==0">{{success}}</div>
     <div class="col-md-3 ">
     <book :book="book" ></book>
    <author :author="author" ></author>
    <genre :genre="genre" ></genre>
    
     </div>
   
    </div>
   
  </div>

</template>

<script>
import axios from 'axios'
import Login from './Login'
import Author from './Author'
import Genre from './Genre'
import Book from './Book'
export default {
  name: 'Main',
  data () {
    return {
      books: '0',
      books: [],
      authors: [],
      author:'',
      genre:'',
      book:'',
      genres: '0',
      errors: '',
      checkUser: '',
      count: 1,
      add: '',
      success: '',
      config: {
                headers: {'Content-Type': 'application/x-www-form-urlencoded'
                    }
              },
    }
  },
  methods: {
   
    getAllBooks: function(){
      var self = this
          axios.get('http://bookshop/user2/bookShop/client/api/books/', this.config)
            .then(function (response) {
              if (response.status == 200) {
                  self.books = response.data;
              }
            else{
              self.errors = response.data
            }
        })
        .catch(function (error) {
          console.log(error)
        });
    },
     getCheck: function(){
                var self = this
                if (localStorage['id'] && localStorage['hash'])
                {
                    self.checkUser = 1
                }
                else{
                    self.checkUser = ''
                }
            },
     getAllGenres: function(){
      var self = this
          axios.get('http://bookshop/user2/bookShop/client/api/genres/', this.config)
            .then(function (response) {
             //console.log(response.data)
              if (response.status == 200) {
                  self.genres = response.data;
              }
            else{
              self.errors = response.data
            }
        })
        .catch(function (error) {
          console.log(error)
        });
    },
    getAllAuthors: function(){
      var self = this
          axios.get('http://bookshop/user2/bookShop/client/api/authors/', this.config)
            .then(function (response) {
             //console.log(response.data)
              if (response.status == 200) {
                  self.authors = response.data;
              }
            else{
              self.errors = response.data
            }
        })
        .catch(function (error) {
          console.log(error)
        });
    },
    getAuthorById: function($id){
      var self = this
     axios.get('http://bookshop/user2/bookShop/client/api/authors/' + $id)
        
            .then(function (response) {
               console.log(response)
            self.author = response.data[0]            
        })
    },
    getGenresById: function($id){
      var self = this
     axios.get('http://bookshop/user2/bookShop/client/api/genres/' + $id)
        
            .then(function (response) {
               console.log(response)
            self.genre = response.data[0]            
        })
    },
     getBookById: function($id){
      var self = this
     axios.get('http://bookshop/user2/bookShop/client/api/books/' + $id)
        
            .then(function (response) {
               console.log(response)
            self.book = response.data[0]            
        })
    },
  },

  created(){
    this.getAllBooks(),
    this.getAllGenres(),
    this.getAllAuthors(),
    this.getAuthorById(),
    this.getGenresById(),
    this.getBookById(),
    this.getCheck()
  
  },
  computed:{},
    components:{
          'Author': Author,
           'Genre': Genre,
           'Book': Book,
           'loginForm': Login

    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .left-menu{
    padding-top:25px;
  }
   .left-menu li {
     color:Black;
     font-size:24px;
  }
  .left-menu li a{
    font-size:20px;
  }
  .book-list img {
    padding-top: 10px;
    padding-bottom: 20px;
  }
  .book-list p span {
    font-weight:bold;
    font-size:19px;
  }
  .book-list p  {
    color:#535353;
    font-size:16px;
  }
  .main{
   background-color:#00FA9A;
  }
</style>