<template>
  <div>
    <v-row>
      <v-col cols="12">
        <v-card>
          <v-card-title
            >{{ subject }} <v-spacer></v-spacer>
            <v-chip v-if="is_done == 1" label color="success"
              >Sudah Mengerjakan</v-chip
            >
            <v-chip v-else label color="error"
              >Belum Mengerjakan</v-chip
            ></v-card-title
          >
          <v-divider></v-divider>
          <v-card-text>
            <v-row>
              <v-col cols="12" md="6">
                <h3>{{ task_name }}</h3>
                <br />
                <p><b>Detail :</b></p>
                <p>{{ description }}</p>
                <p><b>Batas Pengumpulan :</b></p>
                <p>{{ deadline | waktu }}</p>
                <div v-show="is_done">
                  <p><b>Jawaban :</b></p>
                  <p>{{ hasil }}</p>
                  <p>Waktu Selesai : {{ time_finished | waktu }}</p>
                </div>
              </v-col>
              <v-col cols="12" md="6">
                <img
                  v-if="type_file == 'image'"
                  :src="attachment_file"
                  style="width: 100%"
                  alt=""
                />
                <iframe
                  v-else-if="type_file == 'pdf'"
                  :src="attachment_file"
                  frameborder="0"
                  width="100%"
                  height="500px"
                ></iframe>
              </v-col>
            </v-row>
          </v-card-text>
          <v-divider></v-divider>
          <v-card-actions>
            <v-btn
              v-if="!is_done"
              color="primary"
              block
              @click="kumpulkan_tugas"
              >Kumpulkan Jawaban</v-btn
            >
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
    <dialog-submit ref="ref_dialog_submit"></dialog-submit>
  </div>
</template>
<script>
import dialogSubmit from '@/components/task/dialog-submit.vue'
const moment = require('moment')
moment.locale('id')
export default {
  components: {
    'dialog-submit': dialogSubmit,
  },
  filters: {
    waktu(value) {
      if (!value) return ''
      value = value.toString()
      return moment(value).format('DD MMMM YYYY - HH:mm')
    },
  },
  data() {
    return {
      id: '',
      task_name: '',
      description: '',
      attachment_file: '',
      type_file: '',
      subject: '',
      deadline: '',
      is_done: '',
      hasil: '',
      time_finished: '',
    }
  },
  created() {
    const id = this.$route.params.id
    this.get_detail(id)
  },
  mounted() {
    const id = this.$route.params.id
    this.$nuxt.$on('reload_api_detail', () => {
      console.log('reload_api_detail')
      this.get_detail(id)
    })
  },
  methods: {
    get_detail(id = '') {
      this.$axios
        .$get('/task/detail', {
          params: {
            id,
          },
        })
        .then((res) => {
          if (res.success === true) {
            this.id = res.data[0].id
            this.task_name = res.data[0].task_name
            this.description = res.data[0].description
            this.attachment_file = res.data[0].attachment_file
            this.type_file = res.data[0].type_file
            this.subject = res.data[0].subject
            this.deadline = res.data[0].deadline
            this.is_done = res.data[0].is_done
            this.hasil = res.data[0].hasil
            this.time_finished = res.data[0].time_finished
          }
        })
    },
    kumpulkan_tugas() {
      this.$refs.ref_dialog_submit.id_tugas = this.id
      this.$refs.ref_dialog_submit.dialog = true
    },
  },
}
</script>
