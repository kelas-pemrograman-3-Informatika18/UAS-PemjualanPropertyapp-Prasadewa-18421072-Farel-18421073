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
              <div class="text-h6">Edit</div>
              <div >Input Data Property</div>
            </q-banner>
          </div>
        </div>
      </div>
    </div>

    <q-card flat>
      <q-card-section class="row">
        <q-form
        @submit="onSubmit()"
            class="q-col-gutter-md q-col-lg-6 col-md-6 col-xs-12"
            >
            <q-input
                filled
                v-model="form.judulRumah"
                label="Judul Rumah"
                lazy-rules
                :rules="[ val => val && val.length > 0 || 'Masukan Judul Rumah']"
            />

             <q-input
              filled
              v-model="form.harga"
              label="Harga"
              type="number"
              lazy-rules
            />

            <q-input
              filled
              v-model="form.tahunpembuatan"
              label="Tahun Pembuatan"
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Masukan Tahun Pembuatan']"
            />

            <q-select
              filled
              v-model="form.kondisi"
              :options="optionKondisi"
              label="Pilih Kondisi"
              :rules="[ val => val && val.length > 0 || 'Masukan Kondisi']"
            />

            <q-input
              v-model="form.deskripsirumah"
              filled
              type="textarea"
              label="Deskripsi"
              :rules="[ val => val && val.length > 0 || 'Masukan Deskripsi Rumah']"
            />

            <q-file accept=".jpg, image/*" color="teal" filled v-model="image" label="Upload Gambar">
              <template v-slot:prepend>
                <q-icon name="cloud_upload" />
              </template>
            </q-file>

            <div>
                <q-btn label="Submit" type="submit" color="primary"/>
                <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
            </div>

        </q-form>
      </q-card-section>
    </q-card>

  </q-page>
</template>
<script>
export default {
  data () {
    return {
      form: {
        judulRumah: null,
        harga: 0,
        tahunpembuatan: null,
        kondisi: null,
        deskripsirumah: null
      },
      optionKondisi: [
        'Baru',
        'Bekas Pemakaian'
      ],
      image: null
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$axios.get(`property/getbyid/${this.$route.params.id}`)
        .then(res => {
          if (res.data.sukses) {
            this.form = res.data.data
          } else {
            this.$router.push({ name: 'dataProperty' })
          }
        })
    },
    onSubmit () {
      const formData = new FormData()
      formData.append('image', this.image)
      formData.append('data', JSON.stringify(this.form))
      this.$axios.put(`property/edit/${this.$route.params.id}`, formData)
        .then(res => {
          if (res.data.sukses) {
            this.$showNotif(res.data.pesan, 'positive')
            this.$router.push({ name: 'dataProperty' })
          } else {
            this.$showNotif(res.data.pesan, 'negative')
          }
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
