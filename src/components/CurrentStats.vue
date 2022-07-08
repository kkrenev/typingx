<template>
    <div
        :class="{ good: !error && start, bad: error && start }"
        class="current-stats py-2">
        <v-img
            :src="require(`@/assets/img/hand-keyboard.jpeg`)"
            class="image"/>
        <div class="stats py-2">
            <div class="time item">
                <v-icon size="30">mdi-timer-outline</v-icon>
                {{ userStats.seconds }} сек
            </div>
            <div class="speed item">
                <v-icon size="30">mdi-format-letter-case</v-icon>
                {{ userStats.wordPerMinutes }} зн/мин
            </div>
            <div class="errors item">
                <v-icon
                    color="red"
                    size="30">
                    mdi-alert
                </v-icon>
                {{ userStats.errors }} ошбк /
                {{ userStats.errorsPercent }}%
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'current-stats',
        props: {
            userStats: {
                type: Object,
                default: () => {
                },
            },
            error: {
                type: Boolean,
                default: false,
            },
            start: {
                type: Boolean,
                default: false,
            },
        },
    };
</script>

<style lang="scss" scoped>

.current-stats {
    width: 800px;
    height: 100%;
    border: 1px solid #ccc;
    background-color: #FFF;
    margin-top: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    .stats {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 5px;
        font-weight: bold;
        font-size: 30px;

        .item {
            gap: 10px;
            display: flex;
            flex-direction: row;
            align-items: center;
            justify-content: center;
        }
    }

    .image {
        width: 50%;
    }
}

.good {
    border: 1px solid teal;
    background: rgba(0, 128, 128, 0.1);
}

.bad {
    border: 1px solid red;
    background: rgba(255, 0, 0, 0.1);
}
</style>
