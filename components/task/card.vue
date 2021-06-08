<template>
  <v-card outlined>
    <v-card-title>
      Mapel
      <v-spacer></v-spacer>
      <v-chip label color="error">Belum mengerjakan</v-chip>
    </v-card-title>
    <v-divider></v-divider>
    <v-card-text> jenis file </v-card-text>
    <v-divider></v-divider>
    <v-card-text>
      <h3>Judul Tugas</h3>
    </v-card-text>
    <v-divider></v-divider>
    <v-card-actions>
      <v-row>
        <v-col cols="12" md="6" sm="6">
          <div>
            <v-icon>mdi-calendar</v-icon>
            12 Juni 2021
          </div>
        </v-col>
        <v-col cols="12" md="6" sm="6">
          <v-btn style="float: right" color="primary" outlined>Detail</v-btn>
        </v-col>
      </v-row>
    </v-card-actions>
  </v-card>
</template>
