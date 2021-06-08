<template>
  <div class="text-center">
    <v-dialog v-model="dialog" width="500">
      <v-card>
        <v-card-title class="text-h5 grey lighten-2">
          Kirim Jawaban
        </v-card-title>

        <v-card-text>
          <v-textarea
            v-model="jawaban"
            name="jawaban"
            label="Jawaban"
          ></v-textarea>
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            :loading="loading"
            :disabled="loading"
            @click="submit_tugas"
          >
            Simpan
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
export default {
  data() {
    return {
      dialog: false,
      jawaban: '',
      id_tugas: null,
      loading: false,
    }
  },
  methods: {
    submit_tugas() {
      this.loading = true
      this.$axios
        .$post('task/submit', {
          id: this.id_tugas,
          hasil: this.jawaban,
        })
        .then((res) => {
          if (res.success === true) {
            this.$nuxt.$emit('reload_api_detail')
            this.dialog = false
          }
          this.loading = false
        })
    },
  },
}
</script>
