<template>
  <main-layout>
    <template v-slot:drawer>
      <template v-if="activeClass != null">
        <file-info />
      </template>
      <template v-else>
        <v-row align="center" class="mt-5">
          <v-col cols="12" class="text-center">
            Select file or folder
          </v-col>
        </v-row>
      </template>
    </template>

    <v-row class="mt-8">
      <v-col cols="12">
        <span class="subtitle-2">Recent File</span>
      </v-col>
      <v-col cols="12" class="pt-0 d-flex">
        <template v-for="(file, index) in directories">
          <div
            :key="index"
            v-if="file.type === 'file'"
            class="recent-card"
            :class="{ active: index === activeClass ? 'active' : '' }"
            @click="setActive(index)"
            @contextmenu="rightClick($event, index)"
          >
            <v-img
              v-if="file.file_type === 'after_effect'"
              width="80"
              src="../assets/icon/after-effect.svg"
            ></v-img>
            <v-img
              v-if="file.file_type === 'docx'"
              width="80"
              src="../assets/icon/g-docs.svg"
            ></v-img>
            <v-img
              v-if="file.file_type === 'form'"
              width="80"
              src="../assets/icon/g-form.svg"
            ></v-img>
            <v-img
              v-if="file.file_type === 'slides'"
              width="80"
              src="../assets/icon/g-slides.svg"
            ></v-img>
            <v-img
              v-if="file.file_type === 'jpg'"
              width="80"
              src="../assets/icon/xd.svg"
            ></v-img>
            <div class="text-truncate">{{ file.filename }}</div>
          </div>
        </template>
      </v-col>
    </v-row>
    <v-row class="mt-8">
      <v-col cols="12">
        <span class="subtitle-2">Files</span>
      </v-col>
      <v-col cols="12" class="pt-0 d-flex flex-wrap">
        <template v-for="(folder, i) in directories">
          <div
            :key="i"
            v-if="folder.type == 'folder'"
            class="recent-card"
            :class="{ active: i === activeClass ? 'active' : '' }"
            @click="setActive(i)"
            @contextmenu="rightClick($event, i)"
          >
            <v-img width="80" src="../assets/icon/folder.svg"></v-img>
            <div class="text-truncate">{{ folder.file }}</div>
          </div>
        </template>
      </v-col>
    </v-row>

    <v-row class="mt-8">
      <v-col cols="12">
        <v-data-table
          v-model="selected"
          single-select
          :headers="headers"
          :items="directories.filter((val) => val.type !== 'folder')"
          disable-pagination
          hide-default-footer
          @click:row="toggleSelected"
          @contextmenu:row="(e, item) => rightClick(e, item, 'table')"
        >
          <template v-slot:[`item.filename`]="{ item }">
            <v-icon :color="fileTypes[item.file_type].color">
              {{ fileTypes[item.file_type].icon }}
            </v-icon>
            <span class="w-75 text-truncate">
              {{ item.filename }}
            </span>
          </template>
        </v-data-table>
      </v-col>
    </v-row>

    <v-menu
      v-model="showMenu"
      :position-x="x"
      :position-y="y"
      absolute
      offset-y
    >
      <v-list>
        <v-list-item dense v-for="(item, index) in items" :key="index">
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>
          <v-list-item-title>
            {{ item.title }}
          </v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
  </main-layout>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      showMenu: false,
      x: 0,
      y: 0,
      items: [
        { title: "Preview", icon: "remove_red_eye", action: "" },
        { title: "Live Edit", icon: "border_color", action: "" },
        { title: "Edit in Word 365", icon: "insert_drive_file", action: "" },
        { title: "Rename", icon: "format_italic", action: "" },
        { title: "Copy Link", icon: "link", action: "" },
        { title: "Move File", icon: "gamepad", action: "" },
        {
          title: "Start Version Control",
          icon: "format_list_numbered",
          action: "",
        },
        { title: "See Workflow", icon: "swap_horiz", action: "" },
        { title: "Share", icon: "share", action: "" },
        { title: "Document Info", icon: "info", action: "" },
        { title: "Download", icon: "file_download_off", action: "" },
        { title: "Delete File", icon: "delete", action: "" },
      ],
      activeClass: null,
      selected: [],
      fileTypes: {
        docx: { icon: "description", color: "blue" },
        jpg: { icon: "image", color: "grey" },
      },
      imgFileType: {
        docx: "g-docs",
        jpg: "after-effect",
        folder: "folder",
      },
      headers: [
        {
          text: "Name",
          align: "start",
          value: "filename",
          width: "35%",
        },
        { text: "Doc No", value: "doc_no" },
        { text: "Size", value: "size" },
        { text: "Status", value: "file_status" },
        { text: "Upload Date", value: "last_updated" },
        { text: "Last Update", value: "file_last_updated" },
      ],
      directories: [
        {
          id: 7375,
          type: "folder",
          file: "Document generated on Apr 2, 2020 12.24 PM (GMT+7)",
          lower_file: "document generated on apr 2, 2020 12.24 pm (gmt+7)",
          doc_no: "",
          lower_doc_no: "",
          filename: "",
          file_type: "",
          size: "",
          size_total: "",
          last_updated: "",
          file_last_updated: "",
          file_status: "",
        },
        {
          id: 7959,
          type: "folder",
          file: "Document generated on Apr 20, 2020 5.19 PM (GMT+7)",
          lower_file: "document generated on apr 20, 2020 5.19 pm (gmt+7)",
          doc_no: "",
          lower_doc_no: "",
          filename: "",
          file_type: "",
          size: "",
          size_total: "",
          last_updated: "",
          file_last_updated: "",
          file_status: "",
        },
        {
          id: 7488,
          type: "folder",
          file: "Document generated on Apr 8, 2020 10.23 AM (GMT+7)",
          lower_file: "document generated on apr 8, 2020 10.23 am (gmt+7)",
          doc_no: "",
          lower_doc_no: "",
          filename: "",
          file_type: "",
          size: "",
          size_total: "",
          last_updated: "",
          file_last_updated: "",
          file_status: "",
        },
        {
          id: 11421,
          type: "folder",
          file: "Document generated on Aug 26, 2020 3.55 PM (GMT+7)",
          lower_file: "document generated on aug 26, 2020 3.55 pm (gmt+7)",
          doc_no: "",
          lower_doc_no: "",
          filename: "",
          file_type: "",
          size: "",
          size_total: "",
          last_updated: "",
          file_last_updated: "",
          file_status: "",
        },
        {
          id: 6601,
          type: "folder",
          file: "Document generated on Feb 17, 2020 3.01 PM (GMT+7)",
          lower_file: "document generated on feb 17, 2020 3.01 pm (gmt+7)",
          doc_no: "",
          lower_doc_no: "",
          filename: "",
          file_type: "",
          size: "",
          size_total: "",
          last_updated: "",
          file_last_updated: "",
          file_status: "",
        },
        {
          id: 6655,
          type: "folder",
          file: "Document generated on Feb 18, 2020 12.04 PM (GMT+7)",
          lower_file: "document generated on feb 18, 2020 12.04 pm (gmt+7)",
          doc_no: "",
          lower_doc_no: "",
          filename: "",
          file_type: "",
          size: "",
          size_total: "",
          last_updated: "",
          file_last_updated: "",
          file_status: "",
        },
        {
          id: 6187,
          type: "folder",
          file: "Document generated on Feb 2, 2020 7.44 PM (GMT+7)",
          lower_file: "document generated on feb 2, 2020 7.44 pm (gmt+7)",
          doc_no: "",
          lower_doc_no: "",
          filename: "",
          file_type: "",
          size: "",
          size_total: "",
          last_updated: "",
          file_last_updated: "",
          file_status: "",
        },
        {
          id: 5855,
          type: "folder",
          file:
            "Free preview documents generated on Jan 21, 2020 8.46 PM (GMT+7)",
          lower_file:
            "free preview documents generated on jan 21, 2020 8.46 pm (gmt+7)",
          doc_no: "",
          lower_doc_no: "",
          filename: "",
          file_type: "",
          size: "",
          size_total: "",
          last_updated: "",
          file_last_updated: "",
          file_status: "",
        },
        {
          id: 4503,
          type: "folder",
          file:
            "Free preview documents generated on Jan 5, 2020 9.06 AM (GMT+7)",
          lower_file:
            "free preview documents generated on jan 5, 2020 9.06 am (gmt+7)",
          doc_no: "",
          lower_doc_no: "",
          filename: "",
          file_type: "",
          size: "",
          size_total: "",
          last_updated: "",
          file_last_updated: "",
          file_status: "",
        },
        {
          id: 6482,
          type: "folder",
          file: "Test 01",
          lower_file: "test 01",
          doc_no: "",
          lower_doc_no: "",
          filename: "",
          file_type: "",
          size: "",
          size_total: "",
          last_updated: "",
          file_last_updated: "",
          file_status: "",
        },
        {
          id: 19407,
          type: "file",
          file: "F-01 Implementation Plan Form (1)",
          lower_file: "f-01 implementation plan form (1)",
          doc_no: "IP20-01",
          lower_doc_no: "ip20-01",
          filename: "IP20-01 F-01 Implementation Plan Form (1)",
          file_type: "docx",
          size: "61.1KB",
          size_total: 62536,
          last_updated: "26 Feb 2020 22:42",
          file_last_updated: "2020-02-26 15:42:41",
          file_status: "Published",
        },
        {
          id: 19331,
          type: "file",
          file: "Software Validation Implementation Plan",
          lower_file: "software validation implementation plan",
          doc_no: "IP20-04",
          lower_doc_no: "ip20-04",
          filename: "IP20-04 Software Validation Implementation Plan",
          file_type: "docx",
          size: "62.9KB",
          size_total: 64401,
          last_updated: "25 Feb 2020 20:28",
          file_last_updated: "2020-02-25 13:28:27",
          file_status: "Published",
        },
        {
          id: 19804,
          type: "file",
          file: "Good Document Practice SOP",
          lower_file: "good document practice sop",
          doc_no: "IP20-05",
          lower_doc_no: "ip20-05",
          filename: "IP20-05 Good Document Practice SOP",
          file_type: "docx",
          size: "58.4KB",
          size_total: 59769,
          last_updated: "07 Dec 2020 05:45",
          file_last_updated: "2020-12-06T22:45:38.000000Z",
          file_status: "Draft (Please set Assignees)",
        },
        {
          id: 25246,
          type: "file",
          file: "Test GDRIVE",
          lower_file: "test gdrive",
          doc_no: "",
          lower_doc_no: "",
          filename: "Test GDRIVE",
          file_type: "docx",
          size: "58.4KB",
          size_total: 59800,
          last_updated: "07 Dec 2020 11:35",
          file_last_updated: "2020-12-07T04:35:06.000000Z",
          file_status: "Draft",
        },
        {
          id: 25265,
          type: "file",
          file: "b469609d1134303d339c09f2fb1bb84b",
          lower_file: "b469609d1134303d339c09f2fb1bb84b",
          doc_no: "",
          lower_doc_no: "",
          filename: "b469609d1134303d339c09f2fb1bb84b",
          file_type: "jpg",
          size: "365.2KB",
          size_total: 373999,
          last_updated: "22 Apr 2020 16:02",
          file_last_updated: "2020-04-22 09:02:02",
          file_status: "Published",
        },
      ],
    }
  },

  methods: {
    setActive(index) {
      if (this.activeClass === index) {
        this.activeClass = null
      } else {
        this.activeClass = index
        this.selected = []
      }
    },

    rightClick(e, indexOrItem, position) {
      e.preventDefault()
      if (position == "table") {
        this.toggleSelected(indexOrItem.item)
      } else {
        if (this.activeClass !== indexOrItem) {
          this.setActive(indexOrItem)
        }
      }

      this.showMenu = false
      this.x = e.clientX
      this.y = e.clientY

      this.$nextTick(() => {
        this.showMenu = true
      })
    },

    toggleSelected(item) {
      this.selected = [item]
      this.activeClass = -1
    },
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

header {
  z-index: 1111 !important;
}

.w-75 {
  width: 75% !important;
}

.theme--light.v-data-table tbody tr.v-data-table__selected {
  background: #e7f3ff !important;
}

.v-list-item--dense,
.v-list--dense .v-list-item {
  min-height: 30px;

  .v-list-item__title {
    font-size: 11px;
    line-height: 12px;
  }
}
</style>
