
<template>
  <div id="body">
    <h2><center><br>Selamat Datang</center></h2>
    <div class="nn">
      <h3>
        <center><br />FORM PEMINJAMAN BUKU</center>
      </h3>

      <form @submit.prevent="add">
        <input type="hidden" v-model="form.id" />
        <label for="form.no">no :</label><br />
        <input type="text" v-model="form.no" required/><br /><br />
        <label for="form.no">Nama Siswa :</label><br />
        <input type="text" v-model="form.name" required/><br /><br />
        <label for="form.judul">Judul Buku :</label><br />
        <input type="text" v-model="form.judul" required><br /><br />
        <label for="form.name">Tanggal Pinjam:</label><br />
        <input type="text" v-model="form.tahun" required><br /><br />
        <label for="form.tahun">Tanggal Pengembalian :</label>
        <input type="text" v-model="form.kategori" required><br /><br />
        <center>
          <button type="submit" v-show="!updateSubmit" id="ml">Add Peminjaman</button>
        </center>
        <button type="button" v-show="updateSubmit" @click="update(form)" id="xo">
          Update</button
        ><br /><br />
      </form>
    </div>
    <div id="ss">
      <h4><center><b>DAFTAR PINJAM BUKU</b></center></h4>

      <table>
        <thead>
          <tr>
            <th id="b">No</th>
            <th id="d">Nama Siswa</th>
            <th id="c">Judul Buku</th>
            <th id="e">Tanggal Pinjam</th>
            <th id="f">Tanggal Pengembalian</th>
            <th id="g">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td id="em">{{ user.no }}</td>
            <td id="mase">{{ user.name }}</td>
            <td id="ac">{{ user.judul }}</td>
            <td id="fis">{{ user.tahun }}</td>
            <td id="sy">{{ user.kategori }}</td>
            <td id="svt">
              <div id="lk">
                <button @click="edit(user)" id="z">Perpanjangan</button>
              </div>
              <div id="kl"><button @click="del(user)" id="v">Kembali</button></div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import axios from "axios";
export default {
  data() {
    return {
      form: {
        id: "",
        no: "",
        name: "",
        judul: "",
        tahun: "",
        kategori: "",
      },
      users: "",
      updateSubmit: false,
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      axios
        .get("http://localhost:3000/users")
        .then((res) => {
          this.users = res.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    add() {
      axios.post("http://localhost:3000/users/", this.form).then((res) => {
        this.load();
        this.form.id = "";
        this.form.no = "";
        this.form.name = "";
        this.form.judul = "";
        this.form.tahun = "";
        this.form.kategori = "";
      });
    },
    edit(user) {
      this.updateSubmit = true;
      this.form.id = user.id;
      this.form.no = user.no;
      this.form.name = user.name;
      this.form.judul = user.judul;
      this.form.tahun = user.tahun;
      this.form.kategori = user.kategori;
    },
    update(form) {
      return axios
        .put("http://localhost:3000/users/" + form.id, { name: this.form.name, no: this.form.no, judul: this.form.judul, tahun: this.form.tahun, kategori: this.form.kategori })
        .then((res) => {
          this.load();
          this.form.id = "";
          this.form.no = "";
          this.form.name = "";
          this.form.judul = "";
          this.form.tahun = "";
          this.form.kategori = "";
          this.updateSubmit = false;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    del(user) {
      axios.delete("http://localhost:3000/users/" + user.id).then((res) => {
        this.load();
        let index = this.users.indexOf(form.name);
        this.users.splice(index, 1);
      });
    },
  },
};
</script>
<style scoped>
#body {
  border: 2px solid black;
  height: 650px;
  background-color: lightseagreen;
}
thead {
  background-color: teal;
}
h2 {
  border: 2px dashed lavenderblush;
  border-radius: 12px;
  font-family: Georgia, 'Times New Roman', Times, serif;
  background-color: navy;
  height: 100px;
  color: whitesmoke;
}
h3 {
  font-family: Georgia, 'Times New Roman', Times, serif;
  border: 1ps solid black;
  background-color: whitesmoke;
  border-top: none;
  width: auto;
  height: 50px;
}
h4 {
  font-family: Georgia, 'Times New Roman', Times, serif;
}
.nn {
  font-family: sans-serif;
  position: absolute;
  left: 200px;
  width: 314px;
  height: auto;
}
#ss {
  font-family: fantasy;
  border: 2px solid black;
  position: absolute;
  right: 200px;
  width: 513px;
  height: auto;
  background-color: linen;
}
#b {
  width: auto;
  text-align: center;
}
#c {
  width: auto;
  text-align: center;
}
#d {
  width: auto;
  text-align: center;
}
#e {
  width: auto;
  text-align: center;
}
#f {
  width: auto;
  text-align: center;
}
#g {
  width: auto;
  text-align: center;
}
#em {
  width: auto;
  text-align: center;
}
#ac {
  width: auto;
  text-align: center;
}
#mase {
  width: auto;
  text-align: center;
}
#fis {
  width: auto;
  text-align: center;
}
#sy {
  width: auto;
  text-align: center;
}
#svt {
  width: auto;
  text-align: center;
  border-top: 2px solid black;

}
#z {
  background-color: rgb(28, 225, 28);
  margin-bottom: 10px;
}
#v {
  background-color: red;
}
#xo {
  background-color: indianred;
}
#ml {
  background-color: slategray;
}
tbody {
  border-top: 2px solid black;
}
</style>