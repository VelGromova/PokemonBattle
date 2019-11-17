<template>
        <div
                class="char"
                :class="[
                  isPlayer && charIsActive ? 'char--attack' : charIsActive,
                  isOpponent && charIsActive ? 'char--damaged' : charIsActive
                ]"
                :style= "{ backgroundImage: this.charImagePath }"
        >
                <div class="effect"></div>
        </div>
</template>

<script>
export default {
  data() {
    return {
        charImgPath : 'url(' + require(`../assets/images/characters/${this.charName}.png`) + ')',
        charImgPathActive: 'url(' + require(`../assets/images/characters/${this.charName}--active.png`) + ')',
    }
  },
  props: {
    isPlayer: Boolean,
    isOpponent: Boolean,
    charIsActive: Boolean,
    charName: String,
    animationName: String,
  },
  computed: {
    charImagePath() {
      return this.isPlayer === true && this.charIsActive === true ? this.charImgPathActive : this.charImgPath;
    }
  },
}
</script>

<style lang="scss">
    .char {
        position: relative;
        width: 330px;
        height: 330px;
        background-repeat: no-repeat;
        background-size: contain;
        transition: background-image 0.3s ease-in-out;
            .effect {
                position: absolute;
                opacity: 0;
                transition: opacity 0.3s ease-in-out;
                z-index: -1;
            }
        &--attack {
            .effect {
                background: url('../assets/images/effects/lightning.png') center no-repeat / contain;
                opacity: 1;
                width: 480px;
                height: 380px;
            }
        }
        &--damaged {
            .effect {
                background: url('../assets/images/effects/explosion.png') center no-repeat / contain;
                transform: translate(-30%, -25%);
                opacity: 1;
                width: 550px;
                height: 500px;
            }
        }
    }

</style>
