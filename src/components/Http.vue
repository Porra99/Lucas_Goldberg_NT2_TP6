<template>
  
  <section class="src-components-http">
    <div class="jumbotron">
    
      <h2>Show Users</h2>
      <hr>
      <br>
      <button class="btn btn-warning my-3 mr-3" @click="getPostsThenCatch()">Get Data (Then Catch)</button>
      <button class="btn btn-success my-3 mr-3" @click="getPostsAsyncAwait()">Get Data (Async Await)</button>
      <br>
      
      <div v-if="posts.length" class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th v-for="(col,index) in getCols" :key="index">{{col}}</th>
          </tr>
          <tr v-for="(post,index) in posts" :key="index">
            <td v-for="(col,index) in getCols" :key="index">{{post[col]}}</td>
          </tr>
        </table>
      </div>

      <h4 v-else-if="click" class="alert alert-danger">No hay usuarios disponibles</h4>
    </div>
  </section>
  
</template>

<script lang="js">
  export default {
    name: 'Http',
    props: [],
    mounted(){

    },
    data(){
      return {
        url : 'https://60dd1cc5c2b6280017febdc2.mockapi.io/LG-TP6',
        posts : [],
        click : false,
      }
    },
    methods:{
      getPostsThenCatch(){
        this.axios(this.url)
        .then(respuesta => {
          this.posts = respuesta.data
          this.click = true
        })
        .catch(error => console.error(error))
      },
      async getPostsAsyncAwait(){
        try{
          let respuesta = await this.axios(this.url)
          this.posts = respuesta.data
          this.click = true
        }
        catch(error){
          console.error(error)
        }
        
      }
    },
    computed: {
      getCols(){
        return Object.keys(this.posts[0])
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="css">

  .jumbotron{
    background-color: rgb(16, 56, 10);
    color: white;
  }

  hr{
    background-color: #eee;
  }

</style>
