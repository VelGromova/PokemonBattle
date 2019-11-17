<template>
    <div class="background">
        <ul class="clouds">
            <li v-for="n in 5" :key="n.id" >
                <img class="clouds__cloud" src="../assets/images/environment/cloud.png">
            </li>
        </ul>
        <slot />
    </div>
</template>

<script>

</script>

<style lang="scss">
.background {
    position: relative;
    background: #076585;
    background: linear-gradient(to top, #fff, #076585);
    box-sizing: border-box;
    height: 100vh;
    overflow: hidden;
    z-index: 1;
    &:before {
        content: '';
        position: absolute;
        left: 0;
        width: 100%;
        height: 100vh;
        background: url('../assets/images/environment/greenValey.png') no-repeat center / cover;
        z-index: -1;
    }
    .clouds {
        &__cloud {
            float: left;
        }

        @for $i from 1 through 10 {
            li:nth-of-type(#{$i}) {
                list-style: none;
                padding-left: #{100 * $i}px;
                position: absolute;
                width: #{500 - ($i * 5)}px;
                height: auto;
                top: random(100) + px;
                animation-name: animateCloud;
                animation-delay: -#{random(100)}s;
                animation-direction: normal;
                animation-iteration-count: infinite;
                animation-timing-function: linear;
                animation-duration: (5 * ($i * 2))+(s);
                opacity: (.25 * $i);
                z-index: -2;
            }
        }
    }

    @keyframes animateCloud {
        0% {
            margin-left: -1000px;
        }
        100% {
            margin-left: 100%;
        }
    }
}

</style>
