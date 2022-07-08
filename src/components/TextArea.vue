<template>
    <div class="textarea">
        <div
            v-for="(str, strId) in strings"
            :key="strId"
            :class="{ current: strId < strIndex }"
            class="text">
            <div
                v-for="(letter, key) in str"
                :key="key"
                :class="{ current: index === key && strIndex === strId, complete: ((key < index && strId <= strIndex) || strId < strIndex) }"
                class="letter-wrapper">
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
            strings: {
                type: Array,
                default: () => [],
            },
            index: {
                type: Number,
                default: 0,
            },
            strIndex: {
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
    background-color: #ebebeb;
    border: 1px solid #aaa;
    border-radius: 12px;
    padding: 12px;
    text-align: left;

    .text {
        font-size: 30px;
        display: flex;
        flex-wrap: wrap;
        margin: 7px 0;
        gap: 0 0;
        height: 28px;
        font-weight: 400;

        .letter-wrapper {
            line-height: 24px;
        }

        .current {
            text-decoration: underline;
            text-underline-offset: 1px;
            color: blue;
        }

        .complete {
            color: #999;
        }
    }
}
</style>
