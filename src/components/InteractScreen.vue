<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((caculatorWindowHeight() - 16 * 4) /
            Math.sqrt(cardsContext.length) -
            16) *
            3) /
            4 +
            16) *
          Math.sqrt(cardsContext.length)
        }px`,
      }"
    >
      <card-flip
        :imgBackFaceUrl="`images/${card}.png`"
        v-for="(card, index) in cardsContext"
        :key="index"
        :card="{ index: index, value: card }"
        :ref="`card-${index}`"
        @onFlip="checkRules($event)"
        :cardsContext="cardsContext"
        :windowHeight="windowHeight"
        :rules="rules"
      />
    </div>
  </div>
</template>

<script>
import CardFlip from "./Card.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardFlip,
  },
  data() {
    return {
      rules: [],
      windowHeight: 750,
    };
  },
  methods: {
    checkRules(card) {
      if (this.rules.length === 2) return false;
      this.rules.push(card);
      if (this.rules.length === 2) {
        if (this.rules[0].value === this.rules[1].value) this.trueRules();
        else {
          this.resetRules();
        }
      }
    },
    resetRules() {
      setTimeout(() => {
        this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
        this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
        this.rules = [];
      }, 800);
    },
    trueRules() {
      this.$refs[`card-${this.rules[0].index}`][0].onEnabledDisableMode();
      this.$refs[`card-${this.rules[1].index}`][0].onEnabledDisableMode();
      this.rules = [];
      const disabledElements = document.querySelectorAll(
        ".screen .card.disabled"
      );
      if (
        disabledElements &&
        disabledElements.length == this.cardsContext.length - 2
      ) {
        setTimeout(() => {
          this.$emit("onFinish");
        }, 920);
      }
    },
    caculatorWindowHeight() {
      this.windowHeight = window.innerHeight;
      return this.windowHeight;
    },
  },
};
</script>
<style scoped>
.screen {
  background-color: var(--dark);
  height: 100vh;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
}
.screen__inner {
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
