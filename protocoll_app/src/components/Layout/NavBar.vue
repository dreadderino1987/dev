<template>
  <nav class="navbar is-success" role="navigation" aria-label="main navigation">
    <div class="container is-max-desktop px-2">
      <div class="navbar-brand">
        <div class="navbar-item is-size-4 is-family-monospace">Notes-App</div>

        <a
          @click.prevent="showMobileNav = !showMobileNav"
          role="button"
          class="navbar-burger"
          :class="{ 'is-active': showMobileNav }"
          aria-label="menu"
          aria-expanded="false"
          data-target="navbarBasicExample"
          ref="navBarBurgerMenuRef"
        >
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>
      <div
        id="navbarBasicExample"
        ref="navBarMenuRef"
        class="navbar-menu"
        :class="{ 'is-active': showMobileNav }"
      >
        <div class="navbar-start">
          <button
            v-if="storeAuth.user.id"
            @click="logout"
            class="button is-small is-info mt-3 ml-5"
          >
            Log out {{ storeAuth.user.email }}
          </button>
        </div>
        <div class="navbar-end">
          <RouterLink
            @click="showMobileNav = false"
            to="/roti"
            class="navbar-item"
            active-class="is-active"
            >Roti</RouterLink
          >
          <RouterLink
            @click="showMobileNav = false"
            to="/"
            class="navbar-item"
            active-class="is-active"
            >Notes</RouterLink
          >
          <RouterLink
            @click="showMobileNav = false"
            to="/stats"
            class="navbar-item"
            active-class="is-active"
            >Stats</RouterLink
          >
          <RouterLink
            @click="showMobileNav = false"
            to="/profile"
            class="navbar-item"
            active-class="is-active"
            >Profile</RouterLink
          >
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref } from "vue";
import { onClickOutside } from "@vueuse/core";
import { useStoreAuth } from "@/stores/storeAuth.js";

const storeAuth = useStoreAuth();

const showMobileNav = ref(false);

const navBarMenuRef = ref(null);
const navBarBurgerMenuRef = ref(null);

onClickOutside(
  navBarMenuRef,
  () => {
    showMobileNav.value = false;
  },
  {
    ignore: [navBarBurgerMenuRef],
  }
);

const logout = () => {
  showMobileNav.value = false;
  storeAuth.logoutUser();
};
</script>

<style>
@media (max-width: 1023px) {
  .navbar-menu {
    position: absolute;
    left: 0;
    width: 100%;
  }
}
</style>
