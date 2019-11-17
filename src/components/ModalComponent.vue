<template>
    <div class="dialog__overlay">
       <div class="dialog__box">
           <h1>{{ title }}</h1>
           <button class="controls__button" @click="action">
                Start new game
           </button>
       </div>
    </div>
</template>

<script>
  export default {
    props: {
      action: Function,
      title: String,
    }
  }
</script>

<style lang="scss">
    .dialog {
        &__overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(52, 117, 33, 0.79);
            z-index: 9;
        }
        &__box {
            position: absolute;
            background: #f7f6ef;
            padding: 20px;
            width: 300px;
            top: 50%;
            left: 50%;
            margin-right: -50%;
            transform: translate(-50%, -50%);
            text-align: center;
            border-radius: 10px;

            .controls__button {
                background: #4BC22B;
                box-shadow: 0 0 5px 0 rgba(0,0,0,0.3);
                border-radius: 5px;
                color: #fff;
                padding: 12px 18px;
                font-size: 1rem;
                margin-top: 1rem;
            }
        }
    }
</style>
