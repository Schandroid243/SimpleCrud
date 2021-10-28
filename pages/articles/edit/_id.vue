<template>
  <b-container>
    <b-row class="d-flex justify-content-center rowTitle">
      <h3> Edit an Article</h3>
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
import axios from 'axios'
import Vue from 'vue'

export default Vue.extend({

  data() {
    return {
      id: '',
      form: {
        title: '',
        description: '',
        author: ''
      },
      show: true,
    }
  },

  // asyncData ({ params }) {
  //   const slug = params.id
  //   return { slug }
  // },

  created() {
    this.id = this.$route.params.id;
  },

  mounted() {
    this.getArticle();
  },

  methods: {
    getArticle() {
      axios.get(`http://localhost:8000/articles/${this.id}`).then((response) => {
        this.form = response.data;
      }).catch((err) => {
        console.log(err);
      })
    },

    submitForm() {
      axios.put(`http://localhost:8000/articles/${this.id}`, this.form).then((response) => {
        console.log(response.data);
        this.$router.go(-1);
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
