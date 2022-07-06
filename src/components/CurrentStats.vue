<template>
    <div class="current-stats py-2">
        <v-img
            :src="require(`@/assets/img/hand-keyboard.jpeg`)"
            class="image py-2"/>
        <div class="stats">
            <div class="time item">
                <v-icon size="30">mdi-timer-outline</v-icon>{{ userStats.seconds }} сек
            </div>
            <div class="speed item">
                <v-icon size="30">mdi-format-letter-case</v-icon>{{ userStats.wordPerMinutes }} зн/мин
            </div>
            <div class="errors item">
                <v-icon
                    size="30"
                    color="red">
                    mdi-alert
                </v-icon>{{ userStats.errors }} / {{ userStats.errorsPercent }}% ошбк
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
                default: () => {},
            },
        },
    };
</script>

<style lang="scss" scoped>
.current-stats {
	height: 100%;
	border: 1px solid #ccc;
	background-color: #f5f5f5;
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
		gap: 10px;
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
</style>
