<template>
    <div class="textarea">
        <div class="text">
            <div
                class="letter-wrapper"
                v-for="(letter, key) in text"
                :class="{ current: index === key }"
                :key="key">
                <span
                    v-if="letter === ' '">&nbsp;</span>
                <span
                    v-else>{{ letter }}</span>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'text-area',
        props: {
            text: {
                type: String,
                default: '',
            },
            index: {
                type: Number,
                default: 0,
            },
        },
    };
</script>

<style lang="scss" scoped>
.textarea {
    width: 800px;
    height: 100%;
    background-color: #cfcfcf;
    border: 1px solid #aaa;
    border-radius: 12px;
    padding: 12px;
    text-align: left;

    .text {
        font-size: 24px;
        display: flex;
        flex-wrap: wrap;
        gap: 1px 0;

        .current {
            outline: 1px solid red;
        }
        
    }
}
</style>
