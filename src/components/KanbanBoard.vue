<template>
  <div id="kanban" class="container m-atas-10">
    <div class="row">
      <kanbanCategory @fetchCategories="fetchCategories" v-for="category in categories" :key="category.id" :category="category"></kanbanCategory>
    </div>
  </div>
</template>

<script>
import axios from '../helpers/axios'
import kanbanCategory from './KanbanCategory'
export default {
  name: 'KanbanBoard',
  data() {
    return {
      categories: []
    }
  },
  components: {
    kanbanCategory
  },
  methods: {
    fetchCategories () {
      axios({
        method: 'GET',
        url: '/category'
      })
        .then(({ data }) => {
          this.categories = data
        })
        .catch(err => {
          console.log(err.response)
          this.$bvToast.toast('Error in fetching categories', {
            title: `Error`,
            variant: 'danger',
            solid: true
          })
        })
    }
  },
  created () {
    this.fetchCategories()
  }
}
</script>

<style>
  .m-atas-10 {
    margin-top: 6rem;
  }
</style>