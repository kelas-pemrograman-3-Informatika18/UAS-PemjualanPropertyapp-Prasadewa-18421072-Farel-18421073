<template>
  <q-layout view="lHh lpR lFf">
    <q-toolbar unelevated style="height: 70px;" class="bg-red-14 text-white">
     <div class="text-h6 q-ml-lg">Aplikasi Penjualan Property</div>

      <q-space />
     <div v-if="$q.screen.md || $q.screen.md || $q.screen.lg || $q.screen.xl">
      <q-btn size="medium" :to="{ name: 'userPage' }" flat>Home</q-btn>
      <q-btn size="medium" :to="{ name: 'myOrder' }" flat>Pesanan Saya</q-btn>
      <q-btn size="medium" flat>Tentang</q-btn>
      <q-btn size="medium" @click="logout()" flat>Logout</q-btn>
     </div>
          <q-btn size="medium" round icon="shopping_cart" flat/>
          <q-btn flat @click="drawer = !drawer" round v-if="$q.screen.xs" icon="menu"/>
    </q-toolbar>
    <q-drawer
        v-model="drawer"
        :width="200"
        :breakpoint="500"
        side="right"
      >
        <q-scroll-area class="fit">
          <q-list padding class="menu-list" >

            <q-item clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="Home" />
              </q-item-section>
              <q-item-section>
                Home
              </q-item-section>
            </q-item>

          </q-list>
        </q-scroll-area>
      </q-drawer>
    <q-page-container class="bg-grey-2">
      <router-view />
    </q-page-container>
 </q-layout>
</template>
<script>
export default {
  data () {
    return {
      drawer: null
    }
  },
  methods: {
    logout () {
      this.$q.localStorage.remove()
      this.$router.push({ name: 'loginPage' })
    }
  }
}
</script>
