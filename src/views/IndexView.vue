<template>
    <div>
        <text-area
            :text="text"
            :index="nowIndex"/>

        <current-stats
            :user-stats="userStats"
            :error="lastLetterIsError"
            :start="start"/>

        <input-area
            :input-value="lastLetter"
            @checkEquals="checkEquals"
            v-if="start"/>
            
        <start-game-button
            v-else
            @start="startGame"
            :timer="startTimer"
            :interval="startInterval"/>
    </div>
</template>

<script>
    import InputArea from '../components/InputArea.vue';
    import TextArea from '../components/TextArea.vue';
    import CurrentStats from '../components/CurrentStats.vue';
    import StartGameButton from '../components/StartGameButton.vue';

    export default {
        components: { TextArea, InputArea, CurrentStats, StartGameButton },
        data() {
            return {
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Impedit molestiae, voluptatum fugit porro nostrum laborum.',
                lastLetter: '',
                nowIndex: 0,
                textArray: [],
                start: false,
                startInterval: 5000,
                startTimer: false,
                secondsInMinutes: 60,
                msInSecond: 1000,
                userStats: {
                    errors: 0,
                    symbols: 0,
                    startTime: '',
                    wordPerMinutes: 0,
                    errorsPercent: 0,
                    seconds: 0,
                },
                sInterval: '',
                lastLetterIsError: false,
            };
        },

        mounted() {
            this.textArray = this.text.split('');
        },

        methods: {
            checkEquals(letter) {
                this.lastLetter = letter.split('').pop();
                const nowLetter = this.textArray.at(this.nowIndex);
                if (nowLetter === this.lastLetter) {
                    this.nowIndex += 1;
                    this.lastLetterIsError = false;
                    if (this.nowIndex >= this.textArray.length) this.finishGame();
                    else this.userStats.symbols += 1;
                } else {
                    this.userStats.errors += 1;
                    this.lastLetterIsError = true;
                }
                this.getWordPerMinutes();
                this.getErrorsPercent();
            },
            startGame() {
                this.userStats = {
                    errors: 0,
                    symbols: 0,
                    startTime: '',
                    wordPerMinutes: 0,
                    errorsPercent: 0,
                    seconds: 0,
                },
                this.startTimer = true;
                setTimeout(() => {
                    this.start = true;
                    this.gameStarted();
                }, this.startInterval);
            },
            gameStarted() {
                this.userStats.startTime = Date.now();
                this.sInterval = setInterval(() => {
                    this.userStats.seconds += 1;
                }, this.msInSecond);
            },
            finishGame() {
                clearInterval(this.sInterval);
                this.getWordPerMinutes();
                this.getErrorsPercent();
                this.start = false;
                this.startTimer = false;
                this.nowIndex = 0;
            },
            getWordPerMinutes() {
                const timeNow = Date.now();
                const timeDiff = timeNow - this.userStats.startTime;
                const wordPerMinutes = this.userStats.symbols / (timeDiff / this.msInSecond) * this.secondsInMinutes;
                this.userStats.wordPerMinutes = wordPerMinutes.toFixed(1);
            },
            getErrorsPercent() {
                const errorsPercent = (this.userStats.errors / this.userStats.symbols * 100).toFixed(1);
                if (errorsPercent >= 100) this.userStats.errorsPercent = 100;
                else this.userStats.errorsPercent = errorsPercent;
            },
        },
    };
</script>

<style lang="scss" scoped></style>
