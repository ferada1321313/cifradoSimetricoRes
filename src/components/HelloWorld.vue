<template>
  <div>
    <h1>DES Encryption</h1>
    <textarea v-model="message" rows="5" cols="40" placeholder="Ingrese su mensaje"></textarea>
    <br>
    <input v-model="key" type="text" placeholder="Ingrese la clave de cifrado (8 caracteres)">
    <br>
    <button @click="encryptMessage">Cifrar</button>
    <button @click="decryptMessage">Descifrar</button>
    <br>
    <div v-if="encryptedMessage">
      <h3>Mensaje Cifrado:</h3>
      <p>{{ encryptedMessage }}</p>
    </div>
    <div v-if="decryptedMessage">
      <h3>Mensaje Descifrado:</h3>
      <p>{{ decryptedMessage }}</p>
    </div>
  </div>
</template>

<script>
import CryptoJS from 'crypto-js';

export default {
  data() {
    return {
      message: '',
      key: '',
      encryptedMessage: '',
      decryptedMessage: '',
    };
  },
  methods: {
    encryptMessage() {
      const message = this.message;
      const key = this.key;

      if (key.length !== 8) {
        alert('Por favor, ingrese una clave de cifrado de 8 caracteres.');
        return;
      }

      const encrypted = CryptoJS.DES.encrypt(message, key);
      this.encryptedMessage = encrypted.toString();
    },
    decryptMessage() {
      const encryptedMessage = this.encryptedMessage;
      const key = this.key;

      if (key.length !== 8) {
        alert('Por favor, ingrese una clave de cifrado de 8 numeros.');
        return;
      }

      const decrypted = CryptoJS.DES.decrypt(encryptedMessage, key);
      this.decryptedMessage = decrypted.toString(CryptoJS.enc.Utf8);
    },
  },
};
</script>


<style>
  #matrix-container {
    margin: 10px;
    text-align: center;
  }

  table {
    border: 2px solid #333;
    border-collapse: collapse;
    margin: 0 auto;
  }

  td {
    border: 1px solid #333;
    padding: 10px;
    text-align: center;
  }
</style>



<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
