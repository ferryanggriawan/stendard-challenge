<template>
  <v-app id="inspire">
    <appbar></appbar>

    <left-navbar></left-navbar>

    <v-navigation-drawer app clipped right color="#fafafa">
      <v-list>
        <template v-for="(menu, i) in menus">
          <template v-if="menu.submenus !== undefined">
            <v-list-group :value="false" no-action sub-group :key="i">
              <template v-slot:activator>
                <v-list-item-content>
                  <v-list-item-title>
                    <v-icon v-text="menu.icon" class="mr-2"></v-icon>
                    <span>{{ menu.title }}</span>
                  </v-list-item-title>
                </v-list-item-content>
              </template>

              <template v-if="menu.type === 'menu'">
                <v-list-item
                  v-for="(submenu, i) in menu.submenus"
                  :key="i"
                  link
                >
                  <v-list-item-icon>
                    <v-icon v-text="submenu.icon"></v-icon>
                  </v-list-item-icon>
                  <v-list-item-title v-text="menu.type"></v-list-item-title>
                </v-list-item>
              </template>
              <template v-else>
                <v-treeview
                  v-model="tree"
                  :open="initiallyOpen"
                  :items="menu.submenus"
                  activatable
                  item-key="name"
                  open-on-click
                >
                  <template v-slot:prepend="{ item, open }">
                    <v-icon v-if="!item.file">
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
              <v-list-item-title v-text="menu.title"></v-list-item-title>
            </v-list-item>
          </template>
        </template>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <!--  -->
    </v-main>
  </v-app>
</template>

<script>
import Appbar from "./components/layout/Appbar.vue"
import LeftNavbar from "./components/layout/LeftNavbar"

export default {
  data() {
    return {
      value: 54,
      bufferValue: 2000,
    }
  },

  components: { LeftNavbar, Appbar },
}
</script>

<style lang="scss">
.v-navigation-drawer__border {
  background-color: #fafafa !important;
}

.v-btn {
  text-transform: none !important;
}

.v-btn--is-elevated {
  box-shadow: 2px 4px 8px rgba(71, 131, 196, 0.1) !important;
}

.v-application--is-ltr .v-list-group--sub-group .v-list-group__header {
  padding: 0 !important;
}

.v-list-item {
  padding: 0 24px !important;
}

.v-list-item__icon.v-list-group__header__prepend-icon {
  margin-right: 0 !important;
}

.v-list-item__icon {
  margin-right: 8px !important;
}

.v-list-group__items .v-treeview .v-treeview-node__root {
  padding-left: 24px;
}

.v-text-field--shaped {
  border-radius: 50px !important;
}

.v-input__slot {
  padding: 0 24px !important;
}

.w-25 {
  width: 25% !important;
}

.v-list-item__title {
  font-size: 0.8rem;
  color: #565656;
}
</style>
