<template>
  <v-app-bar
    app
    clipped-right
    flat
    color="primary"
    dark
    height="56px"
    class="px-6"
  >
    <v-text-field
      placeholder="Search solution..."
      shaped
      solo
      light
      hide-details
      append-icon="search"
      dense
      height="42px"
    ></v-text-field>
    <v-spacer></v-spacer>
    <a href="#" class="white--text mr-2">
      <small>10 Days left for your trial account</small>
    </a>
    <v-btn color="orange" small depressed class="mx-2">Upgrade My Plan</v-btn>
    <div :style="{ width: '250px' }" class="d-flex align-center mx-2">
      <span class="w-25 mr-2">
        <small>
          <div>Used</div>
          <div><b>54 Mb</b></div>
        </small>
      </span>
      <v-progress-linear
        v-model="value"
        color="orange"
        background-color="white"
      ></v-progress-linear>
      <span class="w-25 ml-2">
        <small>
          <div>Total</div>
          <div><b>2 Gb</b></div>
        </small>
      </span>
    </div>
    <v-btn icon>
      <v-icon>business</v-icon>
    </v-btn>
    <v-btn icon>
      <v-icon>notifications_active</v-icon>
    </v-btn>
  </v-app-bar>
</template>

<script>
export default {
  data() {
    return {
      value: 20,
    }
  },
}
</script>

<style lang="scss" scoped></style>
