<template>
  <div id="input_area">
    <input
      @click="this.error = false"
      @keyup.enter="validateAndEmit"
      class="input_area--input"
      v-model="inputValue"
      type="text"
      placeholder="Enter your GitHub user"
    />
    <button class="input_area--btn" type="submit" :disabled="!isValidUsername">
      <div @click="validateAndEmit">OK</div>
    </button>
    <p class="input_area--error" v-if="error">{{ errorMessage }}</p>
  </div>
</template>

<script>
export default {
  name: "input_area",
  data() {
    return {
      inputValue: "",
      error: false,
    };
  },
  computed: {
    isValidUsername() {
      return /^[a-z\d](?:[a-z\d]|-(?=[a-z\d])){0,38}$/i.test(this.inputValue);
    },
    errorMessage() {
      if (this.inputValue === "") {
        return "You must enter a username";
      } else {
        return "That is not a valid username";
      }
    },
  },
  methods: {
    validateAndEmit() {
      if (this.isValidUsername) {
        this.$emit("userSubmition", this.inputValue);
        this.clearInput();
        return;
      }

      this.error = true;
    },
    clearInput() {
      this.inputValue = "";
    },
  },
};
</script>

<style>
#input_area {
  display: flex;
  position: relative;
  margin-bottom: 20px;
}

#input_area div {
  padding: 6px;
  pointer-events: auto; /*workaround to have click event on disabled btn*/
}

.input_area--input {
  background: transparent;
  border: none;
  outline: none;
  color: rgb(83, 83, 83);
  border-bottom: 1px solid gray;
  text-align: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-weight: bold;
}

.input_area--input:focus {
  border: none;
}

.input_area--btn {
  border-radius: 12px;
  display: inline-block;
  box-sizing: content-box;
  cursor: pointer;
  outline: none;
  border-width: 2px;
  padding: 0;
  margin-left: 20px;
  height: 30px;
  width: 40px;
  color: rgb(83, 83, 83);
  background-color: rgb(193, 231, 233);
  font-weight: bold;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

.input_area--btn:active {
  border: 2px solid rgb(153, 210, 212);
  background-color: rgb(215, 236, 238);
}

.input_area--btn:disabled {
  border: 2px solid rgb(182, 182, 182);
  background-color: rgb(223, 223, 223);
}

.input_area--error {
  position: absolute;
  top: 25px;
  left: 23px;
  background-color: rgb(212, 153, 153);
  padding: 5px 10px;
  border-radius: 10px;
}
</style>