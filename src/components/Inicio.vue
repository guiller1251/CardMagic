<template>
  <div class="inicio">
    <nav id="nav" class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <h2 class="">socialab</h2>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarText"
          aria-controls="navbarText"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarText">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#"
                >BOOTCAMP</a
              >
            </li>
          </ul>
          <span class="navbar-text">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <a class="nav-link active" aria-current="page" href="#"
                  >Inicio</a
                >
              </li>
              <li class="nav-item">
                <a
                  class="nav-link active"
                  aria-current="page"
                  style="color: blue"
                  >Cursos</a
                >
              </li>
              <li class="nav-item">
                <a
                  class="nav-link active"
                  style="background-color: gainsboro; border-radius: 25px"
                  aria-current="page"
                  href="#"
                  ><svg
                    xmlns="http://www.w3.org/2000/svg"
                    width="25"
                    height="25"
                    fill="currentColor"
                    class="bi bi-person-fill"
                    viewBox="0 0 16 16"
                  >
                    <path
                      d="M3 14s-1 0-1-1 1-4 6-4 6 3 6 4-1 1-1 1H3zm5-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6z"
                    /></svg
                ></a>
              </li>
            </ul>
          </span>
        </div>
      </div>
    </nav>
    <hr id="primerHR" />
    <br />
    <div class="container">
      <div class="row" style="float: left">
        <div class="col">
          <p>Inicio/Cursos</p>
        </div>
      </div>
    </div>

    <br /><br />

    <div class="container">
      <div class="row">
        <div class="col">
          <h1 style="font-weight: bold">Cursos</h1>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="row" style="text-align: -webkit-center">
        <div class="col">
          <hr id="segundoHR" />
        </div>
      </div>
    </div>
    <br />
    <div class="container">
      <div class="row">
        <div class="col">
          <p style="font-weight: 600">
            Tincidunt Velit, ullamcorper id vitae neque ac. Hac cursus pharetra
            cursus nec. Leo quisque eget arcu vel. Sed quis purus magna ac netus
            vitae neque
          </p>
        </div>
      </div>
    </div>
    <br />
    <br />
    <div class="album py-5 bg-light">
      <div class="container" id="containerBuscador">
        <div class="row">
          <div class="col" style="margin-top: auto">
            <p class="txt-white">Filtrar por:</p>
          </div>
          <div class="col">
            <label for="disabledTextInput" class="form-label txt-white"
              >Tipo</label
            >
            <select
              v-on:change="infoChange()"
              v-model="selectedType"
              id="idCategoria"
              class="form-select form-select-sm"
            >
              <option value="0" selected>selecciones un tipo</option>
              <option
                v-for="typo in typos"
                :key="typo.types"
                v-bind:value="typo"
              >
                {{ typo }}
              </option>
            </select>
          </div>
          <div class="col">
            <label for="disabledTextInput" class="form-label txt-white"
              >Rareza</label
            >
            <select
              v-on:change="infoChange2()"
              v-model="selectedPower"
              id="disabledSelect"
              class="form-select form-select-sm"
            >
              <option value="0" selected>selecciones una rareza</option>
              <option
                v-for="poder in poderes"
                :key="poder.types"
                v-bind:value="poder"
              >
                {{ poder }}
              </option>
            </select>
          </div>
          <div class="col">
            <label for="disabledTextInput" class="form-label txt-white"
              >Buscador</label
            >
            <input
              v-model="search"
              class="form-control form-control-sm inputbuscar"
              type="text"
              placeholder="Que estas buscando..."
              aria-label=".form-control-sm example"
            />
          </div>
        </div>
      </div>
      <br />
      <div class="container">
        <div
          class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-3"
          style="text-align: -webkit-center"
        >
          <div class="col" v-for="todo in filteredCard" :key="todo.imageUrl">
            <div
              class="card shadow-sm"
              style="border-radius: 14px; height: 313px; width: 226px"
            >
              <a v-on:click="info(todo.id, todo)">
                <img
                  :src="todo.imageUrl"
                 
                  :id="'img_' + todo.id"
                />
              </a>
              <!-- <div class="card-body" style="text-align: initial;background-color: black;">
                <p class="card-text" style="color: white">
                  Nombre: {{ todo.name }}
                </p>
                <p class="card-text" style="color: white">
                  Typo: {{ todo.type }}
                </p>
                <p class="card-text" style="color: white">
                  Rareza: {{ todo.rarity }}
                </p>
                <p class="card-text" style="color: white">
                  Poder: {{ todo.power }}
                </p>
              </div>-->
              <br />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
};
</script>

<script>
import axios from "axios";
export default {
  data() {
    return {
      todos: null,
      typos: null,
      search: "",
      poderes: null,
      change: "",
      selectedType: "",
      selectedPower: "",
    };
  },
  mounted() {
    this.getTodos();
  },
  methods: {
   
    info: function (val, data) {
      Swal.fire({
        title: "Nombre: " + data.name,
        html:
          " <img src=" +
          data.imageUrl +
          " /> <br>" +
          "<p id='tipo'>Typo: " +
          data.type +
          " </p>" +
          " <p> Rareza: " +
          data.rarity +
          " </p>" +
          " <p> Poder: " +
          data.cmc +
          " </p>" +
          " <p> Descripcion: " +
          data.originalText +
          " </p>",
        confirmButtonText: "Ok",
      });
    },

    infoChange: function () {
      this.selectedPower = 0;
    },

    infoChange2: function () {
      this.selectedType = 0;
    },

    getTodos() {
      axios
        .get("https://api.magicthegathering.io/v1/cards") ////llamado a la api de magic
        .then((response) => {
          this.todos = response.data.cards;
          var parsedobj = JSON.parse(JSON.stringify(this.todos));
          const unicos = [];
          const unicosPoder = [];

          //////////for para eliminar duplicados
          for (var i = 0; i < parsedobj.length; i++) {
            var datos = parsedobj[i].types[0];
            var poderes = parsedobj[i].rarity;
            if (!unicos.includes(parsedobj[i].types[0])) {
              unicos.push(datos);
            }
            if (!unicosPoder.includes(parsedobj[i].rarity)) {
              unicosPoder.push(poderes);
            }
            
          }
          ///fin del for
          this.poderes = unicosPoder;
          this.typos = unicos;
        })
        .catch((e) => console.log(e));
    },
  },
  computed: {
    ///funcion para filtrar
    filteredCard: function () {
      let filterType = this.selectedType;
      let filterPower = this.selectedPower;
      return this.todos.filter((todo) => {
        if (this.search != "") {
          this.selectedPower = 0;
          this.selectedType = 0;
          return todo.name.match(this.search)  ;
        }
        if (this.selectedType != 0) {
          return !todo.type.indexOf(this.selectedType) ;
        }
        if (this.selectedPower != 0) {
          return !todo.rarity.indexOf(this.selectedPower);
        }

        return todo.imageUrl;
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#tipo {
  margin-top: 8px;
}
.swal2-popup.swal2-modal.swal2-show {
  background-color: darkgrey !important;
  border-radius: 82px !important;
}
.inputbuscar {
  background-color: blue;
  border-color: blue;
  border-bottom: solid white;
  color: white;
}
::-webkit-input-placeholder {
  color: white;
}
#btn-buscar {
  background-color: blue;
  border-color: white;
  border-radius: 20px;
}
.bg-light {
  background-color: #becddc !important;
}
select {
  background-color: blue;
  border-color: blue;
  border-bottom: solid white;
  color: white;
}
.txt-white {
  color: white;
}
#containerBuscador {
  background-color: blue;
  border-radius: 10px;
  margin-top: -77px;
  padding-bottom: 13px;
}
#segundoHR {
  width: 43px;
  height: 3px !important;
  opacity: 1.25;
  color: blue;
  margin: 0rem 0;
}
#idRowNav {
  margin-right: auto;
}
#nav {
  background-color: white !important;
}

#primerHR {
  margin: 0rem 0 !important;
}
</style>
