<template>
  <div>
    <v-row>
      <v-col v-for="(task, index) in tasks" :key="index" cols="12" md="4">
        <card-task :taskcp="task" @to="to_detail"></card-task>
      </v-col>
    </v-row>
  </div>
</template>
<script>
import Card from '@/components/task/card.vue'
export default {
  components: {
    'card-task': Card,
  },
  data() {
    return {
      keyword: '',
      tasks: [],
    }
  },
  created() {
    this.get_task()
  },
  methods: {
    async get_task() {
      await this.$axios
        .$get('/task', {
          params: {
            keyword: this.keyword,
          },
        })
        .then((x) => {
          if (x.success === true) {
            this.tasks = x.data
          }
        })
    },
    to_detail(id) {
      this.$router.push('/task/' + id)
    },
  },
}
</script>
