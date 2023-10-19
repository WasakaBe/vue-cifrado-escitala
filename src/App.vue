<template>
  <div class="container">
    <h2 class="title">Cifrado de Escítala <br> Alan de Jesus </h2>
    <div class="form-container">
      <div class="form-field">
        <label for="message">Mensaje:</label>
        <input type="text" v-model="message" id="message" class="input" />
      </div>
      <div class="form-field">
        <label for="columns">Número de Columnas:</label>
        <input type="number" v-model="numColumns" id="columns" class="input" />
      </div>
    </div>
    <div class="button-container">
      <button @click="encrypt" class="button">Cifrar</button>
      <button @click="decrypt" class="button">Descifrar</button>
    </div>
    <div class="result-container">
      <p class="result">Mensaje Cifrado: {{ encryptedMessage }}</p>
      <p class="result">Mensaje Descifrado: {{ decryptedMessage }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: '',
      numColumns: 3,
      encryptedMessage: '',
      decryptedMessage: '',
    };
  },
  methods: {
    encrypt() {
      const message = this.message.replace(/ /g, ''); // Eliminar espacios en blanco
      const numRows = Math.ceil(message.length / this.numColumns);
      let grid = Array.from({ length: numRows }, () =>
        Array(this.numColumns).fill(' ')
      );

      let index = 0;
      for (let col = 0; col < this.numColumns; col++) {
        for (let row = 0; row < numRows; row++) {
          if (index < message.length) {
            grid[row][col] = message[index];
            index++;
          }
        }
      }

      this.encryptedMessage = grid
        .map((row) => row.join(''))
        .join('');
    },
    decrypt() {
      const message = this.encryptedMessage;
      const numRows = Math.ceil(message.length / this.numColumns);
      let grid = Array.from({ length: numRows }, () =>
        Array(this.numColumns).fill(' ')
      );

      let index = 0;
      for (let col = 0; col < this.numColumns; col++) {
        for (let row = 0; row < numRows; row++) {
          grid[row][col] = message[index];
          index++;
        }
      }

      this.decryptedMessage = grid
        .map((row) => row.join(''))
        .join('');
    },
  },
};
</script>
<style scoped>
.container {
  text-align: center;
  margin: 30px auto;
  padding: 20px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  max-width: 400px;
  background-color: #f7f7f7;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

.title {
  font-size: 24px;
  color: #333;
  margin-bottom: 20px;
}

.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}

.form-field {
  margin-bottom: 10px;
}

label {
  font-size: 16px;
  color: #555;
  margin-bottom: 6px;
}

.input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 14px;
  width: 100%;
}

.button-container {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}

.button {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  background-color: #007BFF;
  color: #fff;
}

.button:hover {
  background-color: #0056b3;
}

.result-container {
  margin-top: 20px;
}

.result {
  font-size: 16px;
  margin-bottom: 10px;
  color: #333;
}
</style>
