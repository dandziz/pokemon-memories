<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div
    class="card"
    :class="{ disabled: isDisabled }"
    :style="{
      height: `${
        (windowHeight - 16 * 4) / Math.sqrt(cardsContext.length) - 16
      }px`,
      width: `${
        (((windowHeight - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) /
        4
      }px`,
      perpective: `${
        ((((windowHeight - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) /
          4) *
        2
      }px`,
    }"
  >
    <div
      class="card__inner"
      :class="{ 'is-flipped': isFlipped === true }"
      @click="onToggleFlipCard()"
    >
      <div class="card__face card__face--front">
        <div
          class="card__content"
          :style="{
            backgroundSize: `${
              (((windowHeight - 16 * 4) / Math.sqrt(cardsContext.length) - 16) *
                3) /
              4 /
              3
            }`,
          }"
        ></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url('${require('@/assets/' + imgBackFaceUrl)}')`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isFlipped: false,
      isDisabled: false,
    };
  },
  methods: {
    onToggleFlipCard() {
      if (this.rules.length >= 2) return;
      if (this.isDisabled === true) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) {
        this.$emit("onFlip", this.card);
      }
    },
    onFlipBackCard() {
      this.isFlipped = false;
    },
    onEnabledDisableMode() {
      this.isDisabled = true;
    },
  },
  props: {
    imgBackFaceUrl: {
      type: String,
      required: true,
    },
    card: {
      type: [String, Number, Array, Object],
      require: true,
    },
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
    windowHeight: {
      type: Number,
    },
    rules: {
      type: Array,
    },
  },
};
</script>

<style scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
}
.card__inner {
  width: 100%;
  height: 100%;
  transition: 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}
.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}

.card__face--front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: contain;
  height: 100%;
  width: 100%;
}
.card__face--back .card__content {
  background-position: center;
  background-size: contain;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}
.card.disabled .card__inner {
  cursor: default;
}
</style>
