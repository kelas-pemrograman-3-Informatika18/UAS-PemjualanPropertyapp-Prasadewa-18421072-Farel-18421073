<template>
  <q-page padding>
    <div class="q-mb-xl">
    <q-carousel

      animated
      v-model="slide"
      arrows
      navigation
      infinite
      swipeable
    >
      <q-carousel-slide :name="1" img-src="https://png.pngtree.com/thumb_back/fh260/background/20190220/ourmid/pngtree-creative-synthesis-city-comic-real-estate-image_8675.jpg" />
      <q-carousel-slide :name="2" img-src="https://perumahancilacap.com/wp-content/uploads/2019/06/ufreviews-1-1.jpg" />
      <q-carousel-slide :name="3" img-src="data:image/jpeg;base64,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" />
      <q-carousel-slide :name="4" img-src="https://img.rea-asia.com/rumah123/premium/1200x630-fit/primary_property/project/1647/1590927033_background_1647.jpg" />
    </q-carousel>
    </div>
    <div class="row q-col-gutter-md">
    <div class="col-md-3 col-xs-12" v-for="(property, i) in data" :key="i">
    <q-card>
      <q-img
        :src="`${$baseImageURL}/${property.image}`"
        :ratio="16/9"
      />

      <q-card-section>
        <q-btn
          fab
          color="blue"
          icon="add_shopping_cart"
          class="absolute"
          unelevated
          style="top: 0; right: 12px; transform: translateY(-50%);"
        />

        <div class="row no-wrap items-center">
          <div class="col text-h6 ellipsis">
            {{property.judulRumah}}
          </div>
        </div>

        <q-rating v-model="property.rating" readonly color="orange-5" :max="5" size="32px" />
      </q-card-section>

      <q-card-section class="q-pt-none">
        <div class="text-black-2 text-caption">
          Rp. {{ property.harga }},-
        </div>
        <div class="text-subtitle1">
          {{property.kondisi}}
        </div>
        <div @click="property.expanded = !property.expanded" class="text-caption text-grey ellipsis-3-lines cursor-pointer">
          Tampilkan Deskripsi Rumah
        </div>
          <q-slide-transition>
            <div v-show="property.expanded">
              <div class="text-grey text-caption">
                {{ property.deskripsirumah }}
              </div>
            </div>
          </q-slide-transition>
          </q-card-section>

      <q-card-actions>
        <q-btn unelevated @click="openDetail(property)" class="full-width" color="primary">
          Pembelian
        </q-btn>
      </q-card-actions>
    </q-card>
    </div>
    </div>
    <q-dialog v-model="dialog" v-if="dialog" position="bottom">
      <q-card style="width: 500px">
        <q-card-section>
          <div class="text-h6">Detail Pembelian</div>
         </q-card-section>
         <q-card-section style="max-height: 50vh;" class="scrool">
         {{ activeData.judulRumah }} Rp. {{ activeData.harga }},-
         <q-form class="q-mt-md">
          <q-input filled type="number" class="q-mb-md" v-model="jumlah" label="Masukan Jumlah"/>
          Rp. {{ total }},-
             <q-file color="teal" class="q-mt-md" filled v-model="image" label="Label">
                 <template v-slot:prepend>
                  <q-icon name="cloud_upload" />
                 </template>
             </q-file>
         </q-form>
         </q-card-section>
         <q-card-actions align="right">
          <q-btn flat label="Batal" v-close-popup/>
          <q-btn color="primary" @click="prosesTransaksi()" label="Proses"/>
         </q-card-actions>
       </q-card>
    </q-dialog>
  </q-page>
</template>
<script>
export default {
  data () {
    return {
      slide: 1,
      stars: 4,
      dialog: false,
      image: null,
      data: [],
      activeData: null,
      jumlah: 1
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$axios.get('property/getall')
        .then(res => {
          if (res.data.sukses) {
            this.data = res.data.data.map(property => {
              return Object.assign(property, {
                expanded: false
              })
            })
          } else {
            this.$showNotif(res.data.pesan, 'negative')
          }
        })
    },
    openDetail (data) {
      this.activeData = data
      this.dialog = true
    },
    prosesTransaksi () {
      const formData = new FormData()
      formData.append('image', this.image)
      formData.append('data', JSON.stringify({
        idUser: this.$q.localStorage.getItem('dataUser')._id,
        idRumah: this.activeData._id,
        harga: this.activeData.harga,
        jumlah: this.jumlah,
        total: this.total
      }))
      this.$axios.post('order/insert', formData)
        .then(res => {
          if (res.data.sukses) {
            this.$showNotif(res.data.pesan, 'positive')
            this.dialog = false
            this.image = null
          } else {
            this.$showNotif(res.data.pesan, 'negative')
          }
        })
    }
  },
  computed: {
    total () {
      return this.activeData.harga * this.jumlah
    }
  }
}
</script>
