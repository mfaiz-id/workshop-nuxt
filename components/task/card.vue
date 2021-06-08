<template>
  <v-card outlined>
    <v-card-title>
      {{ taskcp.subject }}
      <v-spacer></v-spacer>
      <v-chip label color="error">Belum mengerjakan</v-chip>
    </v-card-title>
    <v-divider></v-divider>
    <v-card-text>
      <center>
        <img
          :src="taskcp.attachment_file | image_thumb"
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
          <v-btn style="float: right" color="primary" outlined>Detail</v-btn>
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
    image_thumb(value) {
      if (!value) return ''
      value = value.toString()
      const extensi = value.split('.').pop()
      if (extensi === 'pdf') {
        return '/icon-file/pdf.png'
      } else if (extensi === 'png') {
        return '/icon-file/image.png'
      }
    },
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
}
</script>
