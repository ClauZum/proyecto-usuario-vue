<template>
  <div>
    <div class="container">
      <div class="text-center">
        <b-list-group>
          <b-list-group-item>
            <h1>Usuario</h1>
          </b-list-group-item>
          <b-list-group-item>
            <img v-bind:src="imagenUsuario" rounded="circle" alt="Circle image">
          </b-list-group-item>
          <b-list-group-item>
            <b-list-group>
              <b-list-group-item v-for="item of listaDatosUsuario" :key="item.id">
                <div class>
                  <i class="material-icons">{{item.icono}}</i>
                  {{item.texto}}
                </div>
              </b-list-group-item>
            </b-list-group>
          </b-list-group-item>
          <b-list-group-item>
            <b-button @click="resetUsuario">Reset</b-button>
          </b-list-group-item>
        </b-list-group>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";

export default {
  name: "Usuario",
  data() {
    return {
      dataUsuario: {},
      imagenUsuario: [],
      nombreCompletoUsuario: [],
      listaDatosUsuario: [],
      android: "android"
    };
  },

  mounted() {
    var self = this;
    self.resetUsuario();
  },
  methods: {
    resetUsuario: function() {
      var self = this;
      axios
        .get("https://randomuser.me/api/")
        .then(function(res) {
          self.listaDatosUsuario = [];
          self.dataUsuario = res.data.results[0];
          self.imagenUsuario = self.dataUsuario.picture.large;
          self.listaDatosUsuario.push({
            icono: "person",
            texto:
              self.dataUsuario.name.title +
              " " +
              self.dataUsuario.name.first +
              " " +
              self.dataUsuario.name.last
          });
          self.listaDatosUsuario.push({
            icono: "email",
            texto: self.dataUsuario.email
          });
          self.listaDatosUsuario.push({
            icono: "event",
            texto: self.dataUsuario.dob.date
          });
          self.listaDatosUsuario.push({
            icono: "place",
            texto: self.dataUsuario.location.street
          });
          self.listaDatosUsuario.push({
            icono: "local_phone",
            texto: self.dataUsuario.phone
          });
          self.listaDatosUsuario.push({
            icono: "lock",
            texto: self.dataUsuario.login.password
          });
          console.log("Data: ", self.dataUsuario);
        })
        .catch(function(error) {
          console.log("Error: ", error);
        });
    },
    andres: function() {
      console.log("variable");
      return "user";
    }
  }
};
</script>
