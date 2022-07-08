<template>
    <div class="main">
        <text-area
            :index="strWordIndex"
            :str-index="strIndex"
            :strings="strings"/>

        <current-stats
            :error="inputValueIsError"
            :start="start"
            :user-stats="userStats"/>

        <input-area
            v-if="start"
            :key="defaultKey"
            :error="inputValueIsError"
            :input-value="inputValue"
            @checkEquals="checkEquals"
            @enter="checkEquals"/>

        <start-game-button
            v-else
            :interval="startInterval"
            :timer="startTimer"
            @start="startGame"/>
    </div>
</template>

<script>
    import InputArea from '../components/InputArea.vue';
    import TextArea from '../components/TextArea.vue';
    import CurrentStats from '../components/CurrentStats.vue';
    import StartGameButton from '../components/StartGameButton.vue';

    export default {
        components: {
            TextArea,
            InputArea,
            CurrentStats,
            StartGameButton,
        },
        data() {
            return {
                text: 'clever... He is good... at Maths and always. with it. because I can hardly. understand all these sums and problems.',
                strings: [],
                strIndex: 0,
                strWordIndex: 0,
                inputValue: '',
                nowIndex: 0,
                textArray: [],
                start: false,
                startInterval: 3000,
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
                inputValueIsError: false,
                word: '',
                words: '',
                wordIndex: 0,
                sequence: '',
                goodWord: '',
                defaultKey: 0,
                appKey: 0,
            };
        },

        mounted() {
            this.strings = this.text.split('. ');
            const stringsLength = this.strings.length;
            this.strings = this.strings.map((item, key) => key < stringsLength - 1 ? item + '. ' : item);
            console.log(this.strings, this.text);
            this.textArray = this.text.split('');
            this.words = this.text.split(' ');
            this.word = this.words.at(this.wordIndex);
        },

        methods: {
            checkEquals(letter) {
                if (this.strWordIndex === this.strings.at(this.strIndex).length - 1 && letter === 'enter') {
                    this.pressEnterEndLine();
                    return;
                } else {
                    const nowTypeLetter = letter.split('').pop();
                    const nowLetter = this.textArray.at(this.nowIndex);
                    this.sequence = letter;
                    if (nowLetter === nowTypeLetter) {
                        if (this.strWordIndex === this.strings.at(this.strIndex).length - 1) {
                            this.lastWordInString();
                        } else if (nowTypeLetter === ' ') {
                            this.spaceChecker();
                        } else {
                            if (!this.word.startsWith(this.sequence)) return;
                            this.defaultChecker(letter);
                        }
                        this.wordIterator();
                    } else {
                        this.errorHandler();
                    }
                }
                this.getWordPerMinutes();
                this.getErrorsPercent();
            },
            errorHandler() {
                this.userStats.errors += 1;
                this.inputValueIsError = true;
            },
            wordIterator() {
                this.nowIndex += 1;
                this.inputValueIsError = false;
                if (this.nowIndex >= this.textArray.length) this.finishGame();
                else this.userStats.symbols += 1;
            },
            defaultChecker(letter) {
                this.strWordIndex += 1;
                this.inputValue = letter;
                this.goodWord = letter;
            },
            spaceChecker() {
                this.wordIndex += 1;
                this.strWordIndex += 1;
                this.word = this.words.at(this.wordIndex);
                this.inputValue = '';
            },
            lastWordInString() {
                this.strIndex += 1;
                this.wordIndex += 1;
                this.strWordIndex = 0;
                this.inputValue = '';
                this.word = this.words.at(this.wordIndex);
            },
            pressEnterEndLine() {
                this.strIndex += 1;
                this.wordIndex += 1;
                this.strWordIndex = 0;
                this.inputValue = '';
                this.word = this.words.at(this.wordIndex);
                this.nowIndex += 1;
                this.inputValueIsError = false;
                if (this.nowIndex >= this.textArray.length) this.finishGame();
                else this.userStats.symbols += 1;
            },
            startGame() {
                this.userStats = {
                    errors: 0,
                    symbols: 0,
                    startTime: '',
                    wordPerMinutes: 0,
                    errorsPercent: 0,
                    seconds: 0,
                };
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
                this.wordIndex = 0;
                this.word = this.words.at(this.wordIndex);
                this.sequence = '';
                this.inputValue = '';
                this.strIndex = 0;
                this.strWordIndex = 0;
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

<style lang="scss" scoped>

</style>
