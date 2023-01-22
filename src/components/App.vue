<template>
  <div class="container">
    <h1>CSS border-radius Generator</h1>
    <div class="box" :style="{ 'border-radius': borderRadius }"></div>
    <p>top left</p>
    <input type="number" :min="0" placeholder="top left" v-model="topLeft" />
    <p>top right</p>
    <input type="number" :min="0" placeholder="top right" v-model="topRight" />
    <p>bottom right</p>
    <input
      type="number"
      :min="0"
      placeholder="bottom left"
      v-model="bottomLeft"
    />
    <p>bottom left</p>
    <input
      type="number"
      :min="0"
      placeholder="bottom right"
      v-model="bottomRight"
    />
    <button @click="resetValues">Reset</button>
    <p ref="borderRadiusValue">
      border-radius: {{ topLeft }}px {{ topRight }}px {{ bottomLeft }}px
      {{ bottomRight }}px;
    </p>
    <p class="copy" @click="copyToClipboard">Copy to clipboard</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      topLeft: "0",
      topRight: "0",
      bottomLeft: "0",
      bottomRight: "0",
      value: "0",
    };
  },
  methods: {
    resetValues() {
      this.topLeft = "0";
      this.topRight = "0";
      this.bottomLeft = "0";
      this.bottomRight = "0";
    },
    async copyToClipboard() {
      try {
        await navigator.clipboard.writeText(
          this.$refs.borderRadiusValue.textContent
        );
        alert("Text copied to clipboard");
      } catch (err) {
        alert("Failed to copy text: ", err);
      }
    },
  },
  computed: {
    borderRadius() {
      return `${this.topLeft}px ${this.topRight}px ${this.bottomLeft}px ${this.bottomRight}px`;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@500&display=swap");

body {
  font-family: "Roboto", sans-serif;
  display: flex;
  justify-content: center;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 1px solid black;
  max-width: 500px;
  padding: 10px;
}

input {
  background-color: transparent;
  padding: 10px 20px;
  font-family: inherit;
}

.box {
  border: 3px solid black;
  height: 150px;
  width: 150px;
}

button {
  margin-top: 10px;
  padding: 10px 30px;
  font-family: inherit;
}

.copy {
  margin-top: -10px;
  font-size: 13px;
}

.copy:hover {
  text-decoration: underline;
  cursor: pointer;
}
</style>
