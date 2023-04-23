<template>
  <div>
    <div class="hidden" v-if="isLogged">
      <vs-sidebar class="sidebar" hover-expand reduce v-model="active" open>
        <template #logo>
          <img
            class="sidebar-logo"
            src="@/assets/logo2.jpg" alt="f"
          />
        </template>
        <!-- :::::::::::::::::::::: -->
        <!-- SideMenu Item List Goes here -->
        <!-- :::::::::::::::::::::: -->
        <vs-sidebar-item
          id="newevent"
          to="/newevent"
          v-if="isLogged"
          class="newevent"
        >
          <template #icon>
            <box-icon name="plus"></box-icon>
          </template>
          New event
        </vs-sidebar-item>
        <vs-sidebar-item id="dashboard" to="/" v-if="isLogged">
          <template #icon>
            <box-icon name="home-smile"></box-icon>
          </template>
          Home
        </vs-sidebar-item>
        <vs-sidebar-item id="reports" to="/reports" v-if="isLogged">
          <template #icon>
            <box-icon name="stats"></box-icon>
          </template>
          Sales Reports
        </vs-sidebar-item>
      </vs-sidebar>
    </div>

    <div id="nav" class="center examplex">
      <vs-navbar center-collapsed fixed shadow>
        <img
          src="@/assets/logo2.jpg"
          class="app-logo-header"
          alt="img"
        />

        <template #right>
          <vs-button flat to="/login" v-if="!isLogged">Login</vs-button>
          <vs-chip v-if="isLogged" class="login-user-chip">
            <span class="login-user-label">{{ loggedInUserEmail }}</span>
            <vs-button @click="logout()"> Logout</vs-button>
          </vs-chip>
        </template>
      </vs-navbar>
    </div>
    <router-view />
    <div class="footer">
      <!--  -->
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
  computed: {
    ...mapGetters(['isLogged']),
  },
  data() {
    return {
      active: 'dashboard',
      loggedInUserEmail: '',
    };
  },

  methods: {
    logout() {
      this.$store.dispatch('logout');
    },
  },
  watch: {
    isLogged: {
      handler() {
        //on update isLogged get the user email from localStorage
        const loggedInUser = JSON.parse(localStorage.getItem('user'));
        const loggedInUserEmailVal = loggedInUser ? loggedInUser.email : '';
        console.log(loggedInUserEmailVal);
        this.loggedInUserEmail = loggedInUserEmailVal;
      },
      deep: true,
    },
  },
};
</script>

<style src="@/assets/css/style.css" />
