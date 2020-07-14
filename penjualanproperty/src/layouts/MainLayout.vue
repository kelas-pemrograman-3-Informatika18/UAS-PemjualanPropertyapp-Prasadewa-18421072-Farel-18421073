<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="bg-red-14 text-blue-grey-14">
      <q-toolbar>
        <q-btn dense flat @click="leftDrawerOpen = !leftDrawerOpen" round icon="menu"/>
        <q-space></q-space>
        <q-btn flat round>
          <q-avatar>
            <img src="https://w7.pngwing.com/pngs/864/1008/png-transparent-house-logo-real-estate-cartoon-house-angle-3d-computer-graphics-building.png">
          </q-avatar>
          <q-menu>
          <q-list style="min-width: 100px">
            <q-separator />
            <q-item clickable v-close-popup>
              <q-item-section>Profile</q-item-section>
            </q-item>
            <q-separator />
            <q-item clickable v-close-popup @click="logout()">
              <q-item-section>Logout</q-item-section>
            </q-item>
          </q-list>
        </q-menu>
        </q-btn>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :breakpoint="500"
      content-class="text-white bg-red-14"
    >
    <q-scroll-area class="fit">
        <q-list>
          <q-item class="justify-center text-center q-mt-md">
            <div>
              <q-avatar size="105px">
                <img src="https://w7.pngwing.com/pngs/864/1008/png-transparent-house-logo-real-estate-cartoon-house-angle-3d-computer-graphics-building.png">
              </q-avatar>
              <div class="text-weight-bold q-mt-md">{{ $q.localStorage.getItem('dataUser').namaLengkap }}</div>
              <div>Aplikasi Penjualan Property</div>
            </div>
          </q-item>

          <q-item clickable active-class="active" v-ripple exact :to="{ name: 'dashboardAdmin' }">
            <q-item-section avatar>
              <q-icon name="dashboard"/>
            </q-item-section>
            <q-item-section>
              <q-item-label>Dashboard</q-item-label>
            </q-item-section>
          </q-item>

          <q-item clickable active-class="active" v-ripple exact :to="{ name: 'dataProperty' }">
            <q-item-section avatar>
              <q-icon name="dashboard"/>
            </q-item-section>
            <q-item-section>
              <q-item-label>Data Property</q-item-label>
            </q-item-section>
          </q-item>

          <q-item clickable active-class="active" :to="{ name: 'inputProperty' }" v-ripple exact>
            <q-item-section avatar>
              <q-icon name="input"/>
            </q-item-section>
            <q-item-section>
              <q-item-label>Input Property</q-item-label>
            </q-item-section>
          </q-item>

          <q-item clickable active-class="active" :to="{ name: 'dataUser' }" v-ripple exact>
            <q-item-section avatar>
              <q-icon name="supervisor_account"/>
            </q-item-section>
            <q-item-section>
              <q-item-label>Data User Property</q-item-label>
            </q-item-section>
          </q-item>

        </q-list>
    </q-scroll-area>
    </q-drawer>

    <q-page-container class="bg-grey-3">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>

export default {
  name: 'MainLayout',

  data () {
    return {
      leftDrawerOpen: false
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
<style scoped>
.active {
  color: black;
  background-color: rgb(239, 239, 245);
}
</style>
