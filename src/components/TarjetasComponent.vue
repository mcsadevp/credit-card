<template>
  <div id="app">
    <form>
      <div>
        <label>Título de la tarjeta: </label>
        <select v-model="tituloTarjeta" class="form-select" aria-label="Default select example">
          <option selected disabled>Selecciona una opción</option>
          <option value="Visa Classic Crédito">Visa Classic Crédito</option>
        </select>
      </div>

      <div>
        <label>Chip SRC: </label>
        <select v-model="chipSRC" class="form-select" aria-label="Default select example">
          <option selected disabled>Selecciona una opción</option>
          <option value ="./assets/chip.png">chip</option>
        </select>
      </div>

      <div>
        <label>Número: </label>
        <input v-model="numeroTarjetaInput" @input="formatNumeroTarjeta" maxlength="19" />
      </div>

      <div>
        <label>Fecha de expiración: </label>
        <input v-model="usuario.fechaExpiracion" type="date"/>
      </div>

      <div>
        <label>Propietario: </label>
        <input v-model="usuario.propietario" />
      </div>

      <div>
        <label>Tipo de tarjeta SRC: </label>
        <select v-model="tipoTarjeta" class="form-select" aria-label="Default select example">
          <option selected disabled>Selecciona una opción</option>
          <option value="./assets/visa.png">Visa</option>
        </select>
      </div>
    </form>

    <div class="carnet">
      <h3>{{ tituloTarjeta }}</h3>
      <img :src="chipSRC" width="40" alt="" />
      <div>
        <h2>{{ formattedNumeroTarjeta }}</h2>
        <span>Fecha Exp: <b>{{ formatoFecha(usuario.fechaExpiracion) }}</b></span>
      </div>
      <footer>
        <span>{{ usuario.propietario }}</span>
        <img :src="tipoTarjeta" width="60" />
      </footer>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TarjetasComponent',
  data() {
    return {
      usuario: {
        propietario: "",
        numeroTarjeta: "",
        fechaExpiracion: "",
      },
      numeroTarjetaInput: "",
      chipSRC: "",
      tipoTarjeta: "",
      tituloTarjeta: "",
    };
  },
  methods: {
    formatoFecha(fecha) {
      if (!fecha) return '';
      const [year, month, day] = fecha.split('-');
      return `${day}/${month}/${year}`;
    },
    formatNumeroTarjeta() {
      let value = this.numeroTarjetaInput.replace(/\s+/g, '').slice(0, 16);
      let formattedValue = '';
      for (let i = 0; i < value.length; i += 4) {
        if (i > 0) formattedValue += ' ';
        formattedValue += value.substring(i, i + 4);
      }
      this.usuario.numeroTarjeta = formattedValue;
      this.numeroTarjetaInput = formattedValue;
    }
  },
  computed: {
    formattedNumeroTarjeta() {
      return this.usuario.numeroTarjeta;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  margin: 0;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 60vh;
  font-size: 10px;
  font-family: sans-serif;
}

#app {
  display: flex;
  gap: 40px;
}

form {
  padding: 18px;
  border-radius: 20px;
  border: ridge 1px;
  box-shadow: 1px 1px 1px 1px gray;
  font-weight: bold;
  display: flex;
  flex-direction: column;
  gap: 15px;
  justify-content: center;
}

form div {
  display: grid;
  grid-template-columns: 100px 200px;
  align-items: center;
  gap: 5px;
}

form div label {
  text-align: right;
}

.carnet {
  width: 400px;
  height: 230px;
  background: #1c1a1e;
  color: white;
  border-radius: 20px;
  padding: 20px;
  box-shadow: 0px 0px 10px 2px black;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

h3 {
  font-size: 20px;
}

h2 {
  font-size: 22px;
  letter-spacing: 10px;
  margin-bottom: 15px;
  text-shadow: 0px 0px 1px gold;
  font-family: Times;
}

b {
  font-size: 16px;
}

footer {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  font-weight: bold;
  font-size: 18px;
  text-transform: uppercase;
  font-style: italic;
}
</style>
