<template>

</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  created() {
    this.$router.push({name: 'articles-add'});
  }
})
</script>
<style scoped>
  .link {
    margin-top: 150px;
    font-size: 25px;
  }
</style>
