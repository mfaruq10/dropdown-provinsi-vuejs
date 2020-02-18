<template>
  <div class="container">
    <div class = "form_dropdown">
      <h2>Dropdown Provinsi</h2>
      <p>Pilih Provinsi, Kota/Kabupaten, dan Kecamatan</p>
      <select class="drop-item" v-model="pilih_provinsi">
          <option value="">-- Pilih Provinsi --</option>
          <option v-for="(index, province) in data_lokasi" :value="province" :key="index">
            {{ province }}
          </option>
      </select>
      <br />
      <select class="drop-item" v-model="pilih_kota" :disabled="kota.length == 0">
          <option value="">-- Pilih Kabupaten / Kota --</option>
          <option v-for="(index, city) in kota" :value="city" :key="index">
            {{ city }}
          </option>
      </select>
      <br />
      <select class="drop-item" v-model="pilih_kecamatan" :disabled="kecamatan.length == 0">
          <option value="">-- Pilih Kecamatan --</option>
          <option v-for="kec in kecamatan" :value="kec" :key="kec">{{ kec }}</option>
      </select>
    </div>
    <div class = "hasil">
      <h3>Result</h3>
      <p v-if="pilih_provinsi&&pilih_kota&&pilih_kecamatan">
          Provinsi {{ pilih_provinsi }}, {{ pilih_kota }}, Kecamatan {{ pilih_kecamatan }}
          <br /><br /></p>
    
      
    </div>
    <br/>
    <marquee>2019 - 2020 Ⓒ Orderpulsa.id All Rights Reserved</marquee>
  </div>
</template>

<script>
export default {
  data: () => ({
    kota: [],
    kecamatan: [],
    pilih_provinsi: '',
    pilih_kota: '',
    pilih_kecamatan: '',
    data_lokasi: {
      'DKI Jakarta': {
        'Kota Jakarta Pusat': ['Kemayoran', 'Menteng', 'Senen'],
        'Kota Jakarta Barat': ['Cengkareng', 'Kebon Jeruk', 'Kalideres'],
        'Kota Jakarta Selatan': ['Kebayoran Baru', 'Mampang Prapatan', 'Setiabudi'],
      },
      'Jawa Timur': {
        'Kota Surabaya': ['Gubeng', 'Rungkut', 'Wiyung'],
        'Kota Malang': ['Blimbing', 'Kedungkandang', 'Lowokwaru'],
        'Kab Tulungagung': ['Tulungagung', 'Kedungwaru', 'Kauman'],
      },      
    },
  }),
  watch: {
    pilih_provinsi() {
      this.kota = [];
      this.kecamatan = [];
      this.pilih_kota = '';
      this.pilih_kecamatan = '';
      if (this.pilih_provinsi.length > 0) {
        this.kota = this.data_lokasi[this.pilih_provinsi];
      }
    },
    pilih_kota() {
      this.kecamatan = [];
      this.pilih_kecamatan = '';
      if (this.pilih_kota.length > 0) {
        this.kecamatan = this.data_lokasi[this.pilih_provinsi][this.pilih_kota];
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  max-width: 700px;
  margin: 0 auto;
}
.form_dropdown {
  padding: 20px;
  width: 700px;
  margin-bottom: 10px;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  border-radius: 5px;
  text-align: center;
  background-color: #657af5
}
.hasil {
  width: 700px;
  padding: 20px;
  box-shadow: 0 4px 8px 0 #7c7c78;
  border-radius: 5px;
  text-align: center;
}
.drop-item {
  width: 600px;
  margin: 10px;
  padding: 10px;
}
h2 {
  color: #000000f8;
  font-family: 'Laila', serif;
}
h4{
  color: rgb(185, 167, 0);
  font-family: 'Times New Roman', Times, serif
}
</style>