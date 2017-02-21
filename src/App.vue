<template>
    <div id="app">
        <section class="hero is-fullheight is-bold is-warning">
            <div class="hero-head">
                <h1 class="title">Pomodoro Timer</h1>
            </div>
            <div class="container hero-body has-text-centered">
                <h1 class="time">{{ minute }} : {{ second }}</h1>
                <a class="button is-primary is-inverted is-outlined" @click="oneSecondPassed">Click</a>
            </div>
        </section>
    </div>
</template>

<script>
    export default {
        name: 'app',
        data () {
            return {
                second: 0,
                minute: 25
            }
        },
        methods: {
            oneSecondPassed () {
                if (this.second === 0) {
                    if (this.minute === 0) {
                        return;
                    }
                    this.second = 59;
                    this.minute -= 1;
                }
                else {
                    this.second -= 1;
                }
            }
        }
    }
</script>

<style lang="scss">
    @import "css/bulma/utilities/_all.sass";
    @import "css/bulma/base/_all.sass";
    @import "css/bulma/layout/_all.sass";
    @import "css/bulma/elements/_all.sass";
    @import "css/bulma/grid/_all.sass";

    .title {
        margin-top: 20px;
        margin-left: 40px;
    }

    .time {
        font-size: 30px;
    }
</style>
