<template>
    <div>
        Great answer! Wanna more?
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