<template>
    <div id="app">
        <section class="hero is-fullheight is-bold is-warning">
            <div class="hero-head">
                <h1 class="title">Pomodoro Timer</h1>
            </div>
            <div class="container hero-body">
                <div class="main has-text-centered">
                    <div class="container">
                        <div class="columns">
                            <div class="column">
                                <h1 class="time">{{ time }}</h1>
                            </div>
                        </div>
                        <div class="columns">
                            <div class="column">
                                <a class="button is-warning is-inverted is-outlined is-large" @click="subtractMinute">-</a>
                                <a class="button is-warning is-inverted is-outlined is-large long-button" @click="reset">Reset</a>
                                <a class="button is-warning is-inverted is-outlined is-large" @click="addMinute">+</a>
                            </div>
                        </div>
                        <div class="columns">
                            <div class="column">
                                <a class="button is-warning is-inverted is-outlined is-large" @click="set(10)">10</a>
                                <a class="button is-warning is-inverted is-outlined is-large long-button" @click="start">Start</a>
                                <a class="button is-warning is-inverted is-outlined is-large" @click="set(25)">25</a>
                            </div>
                        </div>
                    </div>
                </div>
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
                minute: 25,
                defaultLength: 25,
                timer: null
            }
        },
        methods: {
            oneSecondPassed() {
                if (this.second === 0) {
                    if (this.minute === 0) {
                        clearInterval(this.timer);
                        this.notifyUser();
                        return;
                    }
                    this.second = 59;
                    this.minute -= 1;
                }
                else {
                    this.second -= 1;
                }
            },
            start() {
                this.timer = setInterval(this.oneSecondPassed, 1000);
            },
            reset() {
                clearInterval(this.timer);
                this.minute = this.defaultLength;
                this.second = 0;
            },
            addMinute() {
                this.defaultLength += 1;
                this.reset();
            },
            subtractMinute() {
                if (this.defaultLength > 1) {
                    this.defaultLength -= 1;
                }
                this.reset();
            },
            set(num) {
                this.defaultLength = num;
                this.reset();
            },
            notifyUser() {
                if (Notification.permission === "granted") {
                    new Notification("Time's Up");
                }
            }
        },
        computed: {
            time() {
                let minute = this.minute;
                let second = this.second;
                if (minute <= 9) {
                    minute = '0' + minute;
                }
                if (second <= 9) {
                    second = '0' + second;
                }
                return minute + " : " + second;
            }
        },
        created() {
            Notification.requestPermission();
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
        font-size: 100px;
        font-weight: 100;
    }

    .main {
        margin: auto;
    }

    .long-button {
        width: 80px;
    }
</style>
