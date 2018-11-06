<template>
  <div id="article" class="container">
    <div class="page-header">
      <h1>Firebase and Vue</h1>
    </div>
    <div class="card">
      <div class="card-header">
        <h3>Lista de articulos</h3>
      </div>
      <div class="card-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>Title</th>
              <th>Author</th>
              <th>Delete</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="article in articles" :key="article.id">
              <td>
                <a :href="article.url">{{ article.title }}</a>
              </td>
              <td>{{ article.author }}</td>
              <td>
                <span class="pointer"
                      @click="removeArticle(article)">
                  <i class="fas fa-trash"></i>
                </span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>

</template>

<script>
  import articlesRef from '../main';
  export default {
    name: 'container',
      firebase: {
        articles: articlesRef
      },
    data(){
      return {
        newArticle: {
          title: '',
          author: '',
          url: ''
        }
      }
    },
    methods: {
      addArticle() {
        articlesRef.push(this.newArticle);
          this.newArticle.title = '';
          this.newArticle.author = '';
          this.newArticle.url = '';
      },
      removeArticle(article) {
        articlesRef.child(article['.key']).remove();
      }
    }
  }
</script>

<style>
  
</style>