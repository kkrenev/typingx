<template>
    <div class="start-button">
        <v-btn
            class="button"
            x-large
            @click="setStart"
            :class="{ start: timer, success: !timer }">
            {{ text }}
        </v-btn>
    </div>
</template>

<script>
    export default {
        name: 'start-game-button',
        props: {
            timer: {
                type: Boolean,
                default: false,
            },
            interval: {
                type: Number,
                default: 5000,
            },
        },

        data() {
            return {
                text: 'Start Game',
                defaultInterval: 1000,
            };
        },

        watch: {
            timer() {
                let startValue = this.interval;
                this.text = Math.round(this.interval / this.defaultInterval);
                if (this.timer)
                    setInterval(() => {
                        this.text = Math.round((startValue -= this.defaultInterval) / this.defaultInterval);
                    }, this.defaultInterval);
            },
        },
        methods: {
            setStart() {
                if (!this.timer) this.$emit('start');
            },
        },
    };
</script>

<style lang="scss" scoped>
.button {
	margin-top: 20px;
	font-size: 36px;
}

.start {
    background-color: red !important;
    color: #FFF;
    cursor: not-allowed;
    
}

</style>
