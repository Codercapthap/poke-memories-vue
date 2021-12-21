<template>
  <div class="card" 
    :class="{ disabled: isDisable}"
    :style="{
      height: `${(600 - 16 * 4) / Math.sqrt(cardsContext.length) - 16}px`,
      width: `${((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3 / 4}px`
    }"  
  >
    <div class="card__inner">
      <div class="card__face card__face-front"
      :class="{ 'is-flipped': isFlipped }" 
      @click="onToggleFlipCard"
      >
        <div class="card__content"
          :style="{
            backgroundSize: `${((500 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3 / 4}px
            ${((500 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3 / 4}px`
          }"  
        ></div>
      </div>
      <div class="card__face card__face-back" 
      :class="{ 'is-flipped': isFlipped }" 
      @click="onToggleFlipCard"
      >
        <div class="card__content"
        :style="{ 'backgroundImage': 'url(' + require('@/assets/' + imgBackFaceUrl) + ')'}"
        >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imgBackFaceUrl: {
      type: String,
      required: true,
    },
    card: {
      type: [String, Number, Array, Object],
    },
    cardsContext: {
      type: Array,
      default: function(){
        return []
      }
    }
  },
  data() {
    return {
      isFlipped: false,
      isDisable: false
    }
  },
  methods: {
    onToggleFlipCard(){
      if (this.isDisable) return false
      this.isFlipped = !this.isFlipped
      if (this.isFlipped) this.$emit("onFlip", this.card)
    },
    onFlipBackCard(){
      this.isFlipped = false;
    },
    onDisable(){
      this.isDisable = true;
    }
  }
}
</script>

<style lang="css" scoped>
  .card{
    display: inline-block;
    margin-right: 1rem;
    margin-bottom: 1rem;
  }

  .card__inner{
    width: 100%;
    height: 100%;
    transform-style: preserve-3d;
    cursor: pointer;
    position: relative;
  }

  .card__face{
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    overflow: hidden;
    border-radius: 1rem;
    padding: 1rem;
    box-shadow: 0 4px 12px 4px rgba(0, 0, 0, 0.3);
  }

  .card__face-front .card__content{
    background: url("../assets/images/icon_back.png") no-repeat center center;
    height: 100%;
    width: 100%;
  }

  .card__face-back .card__content{
    background-size: contain;
    background-position: center center;
    background-repeat: no-repeat;
    height: 100%;
  }

  .card__face-back, .card__face-front{
    transition: transform 1s;
  }

  .card__face-back{
    background-color: var(--light);
    transform: rotateY(-180deg);
  }

  .card__face-back.is-flipped{
    transform: rotateY(0deg);
  }

  .card__face-front.is-flipped{
    transform: rotateY(-180deg);
  }

  .card.disabled .card__inner{
    cursor: default;
  }
</style>