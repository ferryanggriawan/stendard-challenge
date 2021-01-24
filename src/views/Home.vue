<template>
  <main-layout>
    <template v-slot:drawer>
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
    </template>
    <v-row class="mt-8">
      <v-col cols="12">
        <span class="subtitle-2">Recent File</span>
      </v-col>
      <v-col cols="12" class="pt-0 d-flex">
        <div class="recent-card active">
          <v-img width="80" src="../assets/icon/xd.svg"></v-img>
          <div class="text-truncate">Mockups asdasdasd</div>
        </div>
        <div class="recent-card ">
          <v-img width="80" src="../assets/icon/xd.svg"></v-img>
          <div class="text-truncate">Mockups asdasdasd</div>
        </div>
      </v-col>
    </v-row>
    <v-row class="mt-8">
      <v-col cols="12">
        <span class="subtitle-2">Files</span>
      </v-col>
      <v-col cols="12" class="pt-0 d-flex">
        <div class="recent-card">
          <v-img width="80" src="../assets/icon/folder.svg"></v-img>
          <div class="text-truncate">Mockups Q</div>
        </div>
        <div class="recent-card">
          <v-img width="80" src="../assets/icon/folder.svg"></v-img>
          <div class="text-truncate">Mockups W</div>
        </div>
      </v-col>
    </v-row>

    <v-row class="mt-8">
      <v-col cols="12">
        <v-data-table
          :headers="headers"
          :items="[]"
          disable-pagination
          hide-default-footer
        ></v-data-table>
      </v-col>
    </v-row>
  </main-layout>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      headers: [
        {
          text: "Name",
          align: "start",
          value: "name",
          width: "45%",
        },
        { text: "Doc No", value: "doc_no" },
        { text: "Size", value: "size" },
        { text: "Status", value: "status" },
        { text: "Upload Date", value: "upload_date" },
        { text: "Last Update", value: "last_update" },
      ],
    }
  },
}
</script>
<style lang="scss">
.recent-card {
  width: 90px;
  text-align: center;
  font-size: 12px;
  padding: 10px 10px 15px 10px;
  margin: 0 5px;
  border-radius: 8px;

  &.active {
    background: #e7f3ff;
  }

  .v-image {
    margin: 0 auto;
  }
}

.text-label-value {
  margin-bottom: 24px;

  span {
    color: #4a4a4a;
  }
}
</style>
