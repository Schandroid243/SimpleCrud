<template>
  <b-container>
    <b-row class="d-flex justify-content-center link">
      <b-link :to="{name: 'articles-add'}">
        Create an article
      </b-link>
    </b-row>
  </b-container>
</template>
<style scoped>
  .link {
    margin-top: 150px;
    font-size: 25px;
  }
</style>
