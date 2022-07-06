<template>
    <div class="input">
        <v-text-field
            type="text"
            :value="inputValue"
            @input="onInput"
            outlined
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
            },
        },
    };
</script>

<style lang="scss" scoped>
.input {
	margin-top: 20px;
}
</style>
