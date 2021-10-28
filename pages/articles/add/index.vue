<template>
  <b-container>
    <b-row class="d-flex justify-content-center rowTitle">
      <h3> Create an Article</h3>
    </b-row>
    <b-row align-h="center">
      <b-col cols="12" sm="12">
        <b-form v-if="show" @submit.prevent="submitForm" @reset="resetForm">
          <b-form-group>
            <b-input
              id="title"
              type="text"
              placeholder="Enter a title"
              v-model="form.title">
            </b-input>
          </b-form-group>
          <b-form-group>
            <b-input
              id="description"
              type="text"
              placeholder="Enter a description"
              v-model="form.description">
            </b-input>
          </b-form-group>
          <b-form-group>
            <b-input
              id="author"
              type="text"
              placeholder="Enter an author"
              v-model="form.author">
            </b-input>
          </b-form-group>
          <b-row>
            <b-col cols="12" md="1">
              <b-button type="submit" variant="primary">Submit</b-button>
            </b-col>
            <b-col cols="12" md="2">
              <b-button type="reset">Reset</b-button>
            </b-col>
          </b-row>
        </b-form>
      </b-col>
    </b-row>
  </b-container>
</template>
<script lang="ts">
import Vue from 'vue'
import axios from 'axios'
export default Vue.extend({
  loading: true,
  data() {
    return {
      form: {
        title: '',
        description: '',
        author: ''
      },
      show: true,
    }
  },

  methods: {
    submitForm() {
      axios.post(`http://localhost:8000/articles/`, this.form).then((response) => {
        console.log(response.data);
        this.$router.push({name: 'articles-listArticles'})
      }).catch((err) => {
        console.log(err);
      })
    },
    resetForm() {
      this.form.title = ""
      this.form.description = ""
      this.form.author = ""
    }
  }
})
</script>
<style scoped>
  .rowTitle {
    margin-top: 30px;
  }
</style>
