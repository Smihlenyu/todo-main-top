<template>
  <div class="Drop">
    <button @click="OpenDrop">
      {{ selectedOption.name }}
      <svg
        v-if="dropSel"
        width="9"
        height="5"
        viewBox="0 0 9 5"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M4.63077 4L1.26154 1"
          stroke="#F7F7F7"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M8 1L4.63077 4"
          stroke="#F7F7F7"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
      <svg
        v-if="!dropSel"
        width="9"
        height="5"
        viewBox="0 0 9 5"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M4.63074 1L7.99997 4"
          stroke="#F7F7F7"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M1.26154 4L4.63077 1"
          stroke="#F7F7F7"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
    </button>
    <div class="Drop__menu" v-if="isOpen">
      <div
        class="Drop__item"
        v-for="option in options"
        :key="option.id"
        @click="selectOption(option)"
      >
        <span>{{ option.name }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dropSel: true,
      isOpen: false,
      selectedOption: { id: 1, name: "ALL" },
      options: [
        { id: 1, name: "ALL" },
        { id: 2, name: "Complete" },
        { id: 3, name: "Incomplete" },
        { id: 4, name: "Delete" },
        { id: 5, name: "Delete" },
      ],
    };
  },
  methods: {
    OpenDrop() {
      this.dropSel = !this.dropSel;
      this.isOpen = !this.isOpen;
    },
    selectOption(option) {
      this.selectedOption = option;
      this.isOpen = false;
      this.dropSel = true;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/style/main.scss";

.Drop {
  max-height: 38px;
  & button {
    border-radius: 5px;
    padding: 10px;
    width: 105px;
    height: 38px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: $white;
    background-color: $purple;
    border: none;
    font-family: $font-family;
    font-weight: 500;
    font-size: 12px;
    line-height: 100%;
    text-transform: uppercase;
  }

  & svg {
    margin-right: 3px;
    margin-left: 5px;
  }

  &__menu {
    border: 1px solid $purple;
    border-radius: 5px;
    width: 93px;
    height: auto;
  }
  &__item {
    &:hover {
      background: rgba(108, 99, 255, 0.2);
    }

    & span {
      color: $purple;
      font-family: $font-family;
      font-weight: 400;
      font-size: 16px;
      line-height: 100%;
      text-transform: capitalize;
      cursor: pointer;
      margin-left: 8px;
    }
  }
}
</style>
