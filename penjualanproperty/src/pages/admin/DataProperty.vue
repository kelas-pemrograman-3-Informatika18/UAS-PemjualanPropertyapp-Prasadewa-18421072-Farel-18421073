<template>
  <q-page padding>
    <div class="row q-mb-md col-gutter-md">
      <div class="col-md-12 col-xs-12 col-lg-12">
        <div class="row">
          <div class="col-auto">
            <div class="left"></div>
          </div>
          <div class="col">
            <q-banner inline-actions class="text-blue-grey-15">
              <div class="text-h6">Data Property</div>
              <div >Data Katalog Property Anda</div>
            </q-banner>
          </div>
        </div>
      </div>
    </div>
    <q-card flat>
          <q-table
      :data="data"
      flat
      :columns="columns"
      row-key="name"
    >
        <template v-slot:body="props">
          <q-tr :props="props">
            <q-td key="judulRumah" :props="props">
              {{ props.row.judulRumah }}
            </q-td>
            <q-td key="harga" :props="props">
              {{ props.row.harga }}
            </q-td>
            <q-td key="tahunpembuatan" :props="props">
              {{ props.row.tahunpembuatan }}
            </q-td>
            <q-td key="kondisi" :props="props">
              {{ props.row.kondisi }}
            </q-td>
            <q-td key="deskripsirumah" :props="props">
              <div class="ellipsis" style="max-width: 100px;">
                {{ props.row.deskripsirumah }}
              </div>
            </q-td>
            <q-td key="image" :props="props">
              <q-img
                :src="`${$baseImageURL}/${props.row.image}`"
                spinner-color="white"
                />
            </q-td>
             <q-td key="aksi" :props="props">
                <div class="row q-gutter-md">
                    <q-btn :to="{ name: 'formEditProperty', params: { id: props.row._id }}" label="Edit" icon="edit" color="warning"/>
                    <q-btn @click="deleteProperty(props.row._id)" label="Hapus" icon="delete" color="red"/>
                </div>
            </q-td>

          </q-tr>
        </template>
      </q-table>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      columns: [
        { name: 'judulRumah', align: 'left', label: 'Judul Rumah', field: 'judulRumah', sortable: true },
        { name: 'harga', align: 'left', label: 'Harga', field: 'harga', sortable: true },
        { name: 'tahunpembuatan', align: 'left', label: 'Tahun Pembuatan', field: 'tahunpembuatan', sortable: true },
        { name: 'kondisi', align: 'left', label: 'Kondisi', field: 'kondisi', sortable: true },
        { name: 'deskripsirumah', align: 'left', label: 'Deskripsi Rumah', field: 'deskripsirumah', sortable: true },
        { name: 'image', align: 'left', label: 'Gambar', field: 'image' },
        { name: 'aksi', align: 'left', label: 'Aksi', field: 'aksi' }
      ],
      data: []
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$axios.get('property/getall')
        .then((res) => {
          if (res.data.sukses) {
            this.data = res.data.data
          } else {
            this.$showNotif(res.data.pesan, 'negative')
          }
        })
    },
    deleteProperty (id) {
      this.$q.dialog({
        title: 'Konfirmasi',
        message: 'Yakin Hapus?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.$axios.delete(`property/delete/${id}`)
          .then(res => {
            if (res.data.sukses) {
              this.$showNotif(res.data.pesan, 'positive')
              this.getData()
            } else {
              this.$showNotif(res.data.pesan, 'negative')
            }
          })
      })
    }
  }
}
</script>
<style scoped>
.left {
  width: 4px;
  height: 100%;
  background-color: rgb(24, 175, 4);
}
</style>
