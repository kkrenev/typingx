<template>
    <div class="input">
        <v-text-field
            :value="inputValue"
            autofocus
            outlined
            type="text"
            @input="onInput"
            @keydown.enter="$emit('enter', 'enter')"/>
    </div>
</template>

<script>
    export default {
        name: 'input-area',
        props: {
            inputValue: {
                type: String,
                default: '',
            },
            error: {
                type: Boolean,
                default: false,
            },
        },

        methods: {
            onInput(data) {
                this.$emit('checkEquals', data);
            },

        },
    };
</script>

<style lang="scss" scoped>
.input {
    margin-top: 20px;
}
</style>
