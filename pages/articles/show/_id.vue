<template>
  <b-container>
    <b-row class="d-flex justify-content-center rowTitle">
      <h3>Article Details</h3>
    </b-row>
    <b-row align-h="end" class="rowAddButton">
      <b-col cols="12" md="4">
        <b-link :to="{name: 'articles-listArticles'}">
          <b-button variant="primary">Liste Article</b-button>
        </b-link>
      </b-col>
    </b-row>
    <b-row align-h="center" class="rowData">
      <b-col cols="12" md="9">
        <div>
          <span>Title: </span>
          <span>{{form.title}}</span>
          <span>Description: </span>
          <span>{{form.description}}</span>
          <span>Author: </span>
          <span>{{form.author}}</span>
        </div>
      </b-col>
    </b-row>
  </b-container>
</template>
<script lang="ts">
import Vue from 'vue'
import axios from 'axios'
export default Vue.extend({
  data() {
    return {
      id:'',
      form: {
        title: '',
        description: '',
        author: ''
      }
    }
  },
  created() {
    this.id = this.$route.params._id;
    this.getArticle();
  },
  methods: {
    getArticle() {
      axios.get(`http:localhost:8000/articles/${this.id}`).then((response) => {
        this.form = response.data;
        console.log(this.id);
      }).catch((err) => {
        console.log(err);
      })
    }
  }
})
</script>
<style scoped>
  .rowTitle {
    margin-top: 35px;
  }
  .rowData {
    margin-top: 40px;
  }
  .rowAddButton {
    padding-right: 20px;
  }
</style>
