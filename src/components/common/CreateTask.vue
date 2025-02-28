<template>
  <div class="Create__task">
    <div class="Create">
      <h1>NEW NOTE</h1>
      <input
        type="text"
        placeholder="Input your note..."
        v-model="inputValue"
        v-on:keypress.enter="SendCreateTask"
      />
      <button @click="CloseCreateTask" class="Create__cancel">CANCEL</button>
      <button @click="SendCreateTask" class="Create__apply">APPLY</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: "",
    };
  },
  methods: {
    CloseCreateTask() {
      this.$emit("ClickClose");
    },
    SendCreateTask() {
      if (this.inputValue.trim() !== "") {
        this.$emit("dataSent", this.inputValue);
        this.inputValue = "";
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/style/main.scss";

.Create__task {
  position: absolute;
  z-index: 10;
  left: 50%;
  top: 38%;
  transform: translate(-50%, -50%);
}
.Create {
  border-radius: 16px;
  max-width: 500px;
  width: 100%;
  height: 289px;
  text-align: center;
  display: flex;
  flex-direction: column;
  padding: 18px 30px;
  background-color: $white;
  position: relative;

  margin-top: 30px;
  & h1 {
    margin-bottom: 25px;
  }

  & input {
    border: 1px solid $purple;
    border-radius: 5px;
    padding: 8px 16px;
    width: 440px;
    height: 38px;

    & ::placeholder {
      font-family: $second-family;
      font-weight: 500;
      font-size: 16px;
      line-height: 100%;
      color: #c3c1e5;
    }
  }
  & button {
    position: absolute;
    border-radius: 5px;
    padding: 10px 22px;
    width: 110px;
    height: 38px;
    font-family: $font-family;
    font-weight: 500;
    font-size: 18px;
    line-height: 100%;
    text-transform: uppercase;
  }
  &__cancel {
    bottom: 18px;
    left: 30px;
    border: 1px solid $purple;
    color: $purple;
  }
  &__apply {
    bottom: 18px;
    right: 30px;
    background: $purple;
    border: none;
    color: $white;
  }
}
@import "@/assets/style/main.scss";
</style>
