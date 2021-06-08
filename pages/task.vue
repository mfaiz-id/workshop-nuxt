<template>
  <div>
    <v-row>
      <v-col cols="12" md="3">
        <card-task></card-task>
      </v-col>
      <v-col cols="12" md="3">
        <card-task></card-task>
      </v-col>
      <v-col cols="12" md="3">
        <card-task></card-task>
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
}
</script>
