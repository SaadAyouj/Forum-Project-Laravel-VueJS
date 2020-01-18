<template>

</template>

<script>
export default {
    created(){
        EventBus.$emit('logout');
        this.$noty.warning("Goodbye, see you soon !")
    }
}
</script>

<style>

</style>
