<template>
    <div class="healthbar">
        <h1 class="healthbar__title">{{ charName }}</h1>
        <div class="healthbar__bar">
            {{ charHealth }}
        </div>
    </div>
</template>

<script>
export default {
  props: {
    charName: String,
    charHealth: Number,
    animationName: String,
    player: Object,
  },
}
</script>

<style lang="scss">
    .healthbar {
        &__title {
            margin: 1rem 0;
            font-size: 2rem;
            text-shadow: 1px 1px 5px rgba(105,105,105,0.95);
        }
        &__bar {
            background-color: #4BC22B;
            margin: 0;
            color: #fff;
            line-height: 30px;
            border-radius: 10px;
        }
    }
</style>
