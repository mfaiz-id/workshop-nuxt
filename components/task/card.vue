<template>
  <v-card outlined>
    <v-card-title>
      {{ taskcp.subject }}
      <v-spacer></v-spacer>
      <v-chip v-if="taskcp.is_done == 1" label color="success"
        >Sudah Mengerjakan</v-chip
      >
      <v-chip v-else label color="error">Belum Mengerjakan</v-chip>
    </v-card-title>
    <v-divider></v-divider>
    <v-card-text>
      <center>
        <img
          v-if="taskcp.type_file == 'pdf'"
          src="/icon-file/pdf.png"
          alt=""
          style="width: 30%"
        />
        <img
          v-if="taskcp.type_file == 'image'"
          src="/icon-file/image.png"
          alt=""
          style="width: 30%"
        />
      </center>
    </v-card-text>
    <v-divider></v-divider>
    <v-card-text>
      <h3>{{ taskcp.task_name }}</h3>
    </v-card-text>
    <v-divider></v-divider>
    <v-card-actions>
      <v-row>
        <v-col cols="12" md="6" sm="6">
          <div>
            <v-icon>mdi-calendar</v-icon>
            {{ taskcp.deadline | waktu }}
          </div>
        </v-col>
        <v-col cols="12" md="6" sm="6">
          <v-btn
            style="float: right"
            color="primary"
            outlined
            @click="to_detail(taskcp.id)"
            >Detail</v-btn
          >
        </v-col>
      </v-row>
    </v-card-actions>
  </v-card>
</template>
<script>
const moment = require('moment')
moment.locale('id')
export default {
  filters: {
    waktu(value) {
      if (!value) return ''
      value = value.toString()
      return moment(value).format('DD MMMM YYYY - HH:mm')
    },
  },
  props: {
    taskcp: {
      type: Object,
      required: true,
    },
  },
  methods: {
    to_detail(id) {
      this.$emit('to', id)
    },
  },
}
</script>
