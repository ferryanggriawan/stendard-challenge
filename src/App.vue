<template>
  <v-app id="inspire">
    <appbar></appbar>

    <left-navbar></left-navbar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
import Appbar from "./components/layout/Appbar.vue"
import LeftNavbar from "./components/layout/LeftNavbar"

export default {
  data() {
    return {
      drawer: false,
      value: 54,
      bufferValue: 2000,
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
        },
        {
          title: "Workflow",
          icon: "sync_alt",
        },
        {
          title: "Help",
          icon: "help_outline",
        },
        {
          title: "Audit Trail",
          icon: "list",
        },
        {
          title: "Change Log",
          icon: "history",
        },
      ],
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

  components: {
    LeftNavbar,
    Appbar,
  },

  methods: {
    toggleRightDrawer() {
      this.drawer = !this.drawer
    },
  },
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
  max-width: 260px;
}

.v-text-field--shaped {
  border-radius: 50px !important;
}

.v-toolbar__content .v-input__slot {
  padding: 0 24px !important;
}

.w-25 {
  width: 25% !important;
}

.v-list-item__title {
  font-size: 0.8rem;
  color: #565656;
}

.right-toggle-btn {
  position: absolute;
  right: -1px;
  top: 25px;
  width: 30px;
  height: 75px;
  background: #fafafa;
  z-index: 99;
  display: flex;
  align-items: center;
  border-radius: 8px 0 0 8px;
  justify-items: center;
  justify-content: center;
  cursor: pointer;
}
</style>
