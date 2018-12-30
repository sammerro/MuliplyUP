<template>
    <div>
        <p> Great answer! Wanna more? </p>
        <button @click="onNextButton">
            NEXT
        </button>
    </div>
</template>

<script>

export default {
    methods: {
        onNextButton () {
            this.$emit('nexted');
        }
    }
}
</script>

<style lang="scss" scoped>

</style>