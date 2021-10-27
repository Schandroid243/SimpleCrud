<template>
  <b-container>
    <b-row class="d-flex justify-content-center">
      <h3>Liste Articles</h3>
    </b-row>
    <b-row align-h="end" class="rowAddButton">
      <b-col cols="12" md="4">
        <b-link :to="{name: 'articles-add'}">
          <b-button variant="primary">Create an Article</b-button>
        </b-link>
      </b-col>
    </b-row>
    <b-row align-h="center">
      <b-col cols="12" sm="12">
        <b-table
          id="articleTable"
          class="articleTable"
          :items="listeArticle"
          :fields="fields"
          :per-page="perPage"
          :current-page="currentPage"
          responsive="sm"
          striped>
            <col v-for="article in listeArticle" :key="article._id">
            <template #cell(Title)="article">{{article.item.title}}</template>
            <template #cell(Description)="article">{{article.item.description}}</template>
            <template #cell(Author)="article">{{article.item.author}}</template>

            <template #cell(Action)="article">
              <b-row>
                <b-col cols="8" md="4">
                  <b-link :to="{name: 'articles-edit-id', params: {id: article.item._id}}">
                    <b-button variant="warning">
                      <b-icon icon="pencil-fill"></b-icon>
                    </b-button>
                  </b-link>
                </b-col>
                <b-col cols="8" md="4">
                  <b-link :to="{name: 'articles-show-id', params: {id: article.item._id}}">
                    <b-button variant="primary">
                      <b-icon icon="info-circle-fill"></b-icon>
                    </b-button>
                  </b-link>
                </b-col>
                <b-col cols="8" md="4">
                  <b-button variant="danger" @click="delArticle(article.item._id)">
                      <b-icon icon="trash-fill"></b-icon>
                  </b-button>
                </b-col>
              </b-row>
            </template>

          </b-table>
          <b-pagination
            v-model="currentPage"
            :per-page="perPage"
            :total-rows="rows"
            aria-controls="articleTable">
          </b-pagination>
      </b-col>
    </b-row>
  </b-container>
</template>
<script lang="ts">
import Vue from 'vue'
import axios from 'axios'
import { BootstrapVueIcons } from 'bootstrap-vue'

Vue.use(BootstrapVueIcons);
export default Vue.extend({
  data() {
    return {
      currentPage: 1,
      perPage: 5,
      fields: [
        "Title",
        "Description",
        "Author",
        "Action"
      ],
      listeArticle: []
    }
  },
  created() {
    this.getArticle();
  },
  methods: {
    getArticle() {
      axios.get(`http://localhost:8000/articles/`).then((response) => {
        this.listeArticle = response.data;
        console.log(this.listeArticle);
      }).catch((err) => {
        console.log(err);
      })
    },
    delArticle(articleId: Text) {
      axios.delete(`http://localhost:8000/articles/${articleId}`).then((response) => {
        console.log(response.data);
      }).catch((err) => {
        console.log(err);
      })
    }
  },

  computed: {
    rows(): number {
      return this.listeArticle.length;
    }
  }
})
</script>
<style scoped>
  .rowTitle {
    margin-top: 30px;
  }
  .rowAddButton {
    padding-right: 20px;
  }
  .articleTable {
    margin-top: 25px;
  }
</style>
