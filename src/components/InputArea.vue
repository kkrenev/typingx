<template>
    <div class="input">
        <v-text-field
            type="text"
            :value="inputValue"
            @input="onInput"
            outlined
            class="textarea"
            autofocus/>
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
        },
        methods: {
            onInput(e) {
                this.$emit('checkEquals', e);
                console.log(e);
            },
        },
    };
</script>

<style lang="scss" scoped>
.input {
    margin-top: 20px;
    .textarea {
        border-radius: 12px;
        color: teal;
    }
}
</style>