<template>
  <div class="pa-6">
    <div @click="toggleRightDrawer" class="right-toggle-btn">
      <v-icon>keyboard_arrow_right</v-icon>
    </div>
    <v-navigation-drawer
      v-model="drawer"
      width="325"
      app
      clipped
      right
      color="#fafafa"
    >
      <slot name="drawer"></slot>
    </v-navigation-drawer>
    <template v-if="false">
      <v-breadcrumbs :items="items">
        <template v-slot:divider>
          <v-icon>keyboard_arrow_right</v-icon>
        </template>
      </v-breadcrumbs>
    </template>

    <div class="px-5">
      <v-row>
        <v-col>
          <v-btn depressed class="blue--text" @click="toggleFilter">
            <v-icon class="mr-2">filter_list</v-icon>
            Filter
          </v-btn>
          <v-expansion-panels v-model="panel" multiple flat>
            <v-expansion-panel>
              <v-expansion-panel-content class="pa-6 grey lighten-4">
                <v-row align="end">
                  <v-col cols="3">
                    <label>Document Type</label>
                    <v-text-field
                      hide-details
                      label="Solo"
                      dense
                      solo
                    ></v-text-field>
                  </v-col>
                  <v-col cols="3">
                    <label>Format</label>
                    <v-text-field
                      hide-details
                      label="Solo"
                      dense
                      solo
                    ></v-text-field>
                  </v-col>
                  <v-col cols="3">
                    <label>Author</label>
                    <v-text-field
                      hide-details
                      label="Solo"
                      dense
                      solo
                    ></v-text-field>
                  </v-col>
                  <v-col cols="3">
                    <label>Department</label>
                    <v-text-field
                      hide-details
                      label="Solo"
                      dense
                      solo
                    ></v-text-field>
                  </v-col>
                  <v-col cols="3">
                    <label>Select Category</label>
                    <v-text-field
                      hide-details
                      label="Solo"
                      dense
                      solo
                    ></v-text-field>
                  </v-col>
                  <v-col cols="3">
                    <label>File Status</label>
                    <v-text-field
                      hide-details
                      label="Solo"
                      dense
                      solo
                    ></v-text-field>
                  </v-col>
                  <v-col cols="6">
                    <v-btn color="primary" depressed @click="toggleFilter">
                      Close
                    </v-btn>
                    <v-btn class="mx-3 blue--text" depressed>
                      Reset Filter
                    </v-btn>
                  </v-col>
                </v-row>
              </v-expansion-panel-content>
            </v-expansion-panel>
          </v-expansion-panels>
        </v-col>
      </v-row>

      <slot></slot>
    </div>

    <v-menu offset-y>
      <v-list>
        <v-list-item v-for="(item, index) in 5" :key="index">
          <v-list-item-title>Name</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
  </div>
</template>

<script>
export default {
  data() {
    return {
      panel: [],
      drawer: true,
      items: [
        {
          text: "Dashboard",
          disabled: false,
          href: "breadcrumbs_dashboard",
        },
        {
          text: "Link 1",
          disabled: false,
          href: "breadcrumbs_link_1",
        },
        {
          text: "Link 2",
          disabled: true,
          href: "breadcrumbs_link_2",
        },
      ],
    }
  },

  methods: {
    toggleRightDrawer() {
      this.drawer = !this.drawer
    },

    toggleFilter() {
      if (this.panel.length == 0) {
        this.panel = [0]
      } else {
        this.panel = []
      }
    },

    openMenu(e) {
      console.log("ioe", e.y)
    },
  },
}
</script>

<style lang="scss">
.v-expansion-panel-content__wrap {
  padding: 0 !important;
}

label {
  font-size: 0.8rem;
  display: block;
  margin-bottom: 10px;
}
.v-text-field.v-text-field--solo:not(.v-text-field--solo-flat)
  > .v-input__control
  > .v-input__slot {
  box-shadow: none !important;
}

.v-input {
  font-size: 14px;
}

.v-label {
  font-size: 14px;
}
</style>
