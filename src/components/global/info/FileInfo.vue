<template>
  <div>
    <v-row align="center" no-gutters class="mt-12 px-3">
      <v-col cols="5">
        <span class="white px-3 py-2 rounded green--text">Live Edit</span>
      </v-col>
      <v-col cols="7" class="text-right">
        <v-btn
          shaped
          x-small
          color="white"
          depressed
          class="py-4 mx-1 grey--text"
        >
          <v-icon>file_download</v-icon>
        </v-btn>
        <v-btn
          shaped
          x-small
          color="white"
          depressed
          class="py-4 mx-1 grey--text"
        >
          <v-icon>link</v-icon>
        </v-btn>
        <v-btn
          shaped
          x-small
          color="white"
          depressed
          class="py-4 mx-1 grey--text"
        >
          <v-icon>delete</v-icon>
        </v-btn>
      </v-col>
    </v-row>

    <v-row class="mt-6">
      <v-col cols="12" class="px-8">
        <div class="text-label-value">
          <label class="ma-0 grey--text">Document Name</label>
          <span>Agreement Project Web Series</span>
        </div>
        <div class="text-label-value">
          <label class="ma-0 grey--text">Visibility</label>
          <span>Anyone with the link</span>
        </div>
        <div class="text-label-value">
          <label class="ma-0 grey--text">Owner</label>
          <span>Ahyar Afal Imanudin</span>
        </div>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped></style>
