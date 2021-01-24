<template>
  <v-navigation-drawer v-model="drawer" color="#fafafa" app width="275">
    <v-sheet color="grey lighten-5" width="100%" class="py-14 text-center">
      <v-img
        max-height="50"
        width="150"
        src="../../assets/logo-stendard.svg"
        class="mx-auto"
      ></v-img>
      <v-btn color="white" class="mt-5 primary--text px-8">
        <v-icon size="small" class="mr-1">
          add
        </v-icon>
        Add
      </v-btn>
    </v-sheet>

    <v-list class="left-nav">
      <template v-for="(menu, i) in menus">
        <template v-if="menu.submenus !== undefined">
          <v-list-group :value="false" no-action sub-group :key="i">
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title>
                  <v-icon v-text="menu.icon" class="mr-2"></v-icon>
                  <span>{{ menu.title }}</span>
                  <template v-if="menu.chip !== undefined">
                    <v-chip class="ma-2" x-small>
                      x-small chip
                    </v-chip>
                  </template>
                </v-list-item-title>
              </v-list-item-content>
            </template>

            <template v-if="menu.type === 'menu'">
              <v-list-item v-for="(submenu, i) in menu.submenus" :key="i" link>
                <v-list-item-icon>
                  <v-icon v-text="submenu.icon"></v-icon>
                </v-list-item-icon>
                <v-list-item-title v-text="menu.type"></v-list-item-title>
                <template v-if="menu.chip !== undefined">
                  <v-chip class="ma-2" x-small>
                    x-small chip
                  </v-chip>
                </template>
              </v-list-item>
            </template>
            <template v-else>
              <v-treeview
                v-model="tree"
                :open="initiallyOpen"
                :items="menu.submenus"
                activatable
                item-key="id"
                item-text="text"
                open-on-click
              >
                <template v-slot:prepend="{ item, open }">
                  <v-icon v-if="item.type === 'itsfolder'">
                    {{ open ? "folder_open" : "folder" }}
                  </v-icon>
                  <v-icon v-else>
                    {{ files[item.file] }}
                  </v-icon>
                </template>
              </v-treeview>
            </template>
          </v-list-group>
        </template>

        <template v-else>
          <v-list-item link :key="i">
            <v-list-item-icon>
              <v-icon v-text="menu.icon"></v-icon>
            </v-list-item-icon>
            <v-list-item-title>
              {{ menu.title }}
              <template v-if="menu.chip !== undefined">
                <v-chip color="primary" x-small class="ml-3">
                  {{ menu.chip }}
                </v-chip>
              </template>
            </v-list-item-title>
          </v-list-item>
        </template>
      </template>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
export default {
  data() {
    return {
      drawer: true,
      menus: [
        {
          title: "Ahyar Afal Imanudin",
          icon: "face",
          type: "menu",
          submenus: [{ title: "Sub Menu", icon: "add" }],
        },
        {
          title: "Document Generator",
          icon: "layers",
          type: "menu",
        },
        {
          title: "Library",
          icon: "folder",
          type: "file-tree",
          submenus: [
            {
              id: "folder_7375",
              type: "itsfolder",
              text: "Document generated on Apr 2, 2020 12.24 PM (GMT+7)",
              children: [
                {
                  id: "folder_2222",
                  type: "itsfolder",
                  text: "Forms",
                  children: [],
                },
                {
                  id: "folder_2223",
                  type: "itsfolder",
                  text: "Procedures",
                  children: [],
                },
              ],
            },
            {
              id: "folder_7959",
              type: "itsfolder",
              text: "Document generated on Apr 20, 2020 5.19 PM (GMT+7)",
              children: [],
            },
            {
              id: "folder_7488",
              type: "itsfolder",
              text: "Document generated on Apr 8, 2020 10.23 AM (GMT+7)",
              children: [],
            },
            {
              id: "folder_11421",
              type: "itsfolder",
              text: "Document generated on Aug 26, 2020 3.55 PM (GMT+7)",
              children: [],
            },
            {
              id: "folder_6601",
              type: "itsfolder",
              text: "Document generated on Feb 17, 2020 3.01 PM (GMT+7)",
              children: [],
            },
            {
              id: "folder_6655",
              type: "itsfolder",
              text: "Document generated on Feb 18, 2020 12.04 PM (GMT+7)",
              children: [],
            },
            {
              id: "folder_6187",
              type: "itsfolder",
              text: "Document generated on Feb 2, 2020 7.44 PM (GMT+7)",
              children: [],
            },
            {
              id: "folder_5855",
              type: "itsfolder",
              text:
                "Free preview documents generated on Jan 21, 2020 8.46 PM (GMT+7)",
              children: [],
            },
            {
              id: "folder_4503",
              type: "itsfolder",
              text:
                "Free preview documents generated on Jan 5, 2020 9.06 AM (GMT+7)",
              children: [],
            },
            {
              id: "folder_6482",
              type: "itsfolder",
              text: "Test 01",
              children: [],
            },
          ],
        },
        {
          title: "Workflow",
          icon: "sync_alt",
          type: "menu",
        },
        {
          title: "Help",
          icon: "help_outline",
          type: "menu",
        },
        {
          title: "Audit Trail",
          icon: "list",
          type: "menu",
        },
        {
          title: "Change Log",
          icon: "history",
          type: "menu",
          chip: "New",
        },
      ],
      initiallyOpen: ["public"],
      files: {
        html: "code",
        js: "text_snippet",
        json: "schema",
        md: "language",
        pdf: "picture_as_pdf",
        png: "insert_photo",
        txt: "text_snippet",
        gdrive: "create_new_folder",
        trash: "delete",
        doc: "description",
      },
      tree: [],
    }
  },
}
</script>

<style lang="scss" scoped>
.left-nav {
  max-height: calc(100vh - 220px);
  overflow: auto;
}

.left-nav::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}
.left-nav::-webkit-scrollbar-thumb {
  background-color: #ababab;
}
</style>
