<template>
    <div>
        <div v-bind:key="done.id" v-for="done in dones">
            <DoneItem v-bind:done="done" v-on:del-done="$emit('del-done', done.id)" />
        </div>
    </div>
</template>

<script>
import DoneItem from './DoneItem';
export default {
    name: "Dones",
    components: {
        DoneItem
    },
    props: ["dones"]
}
</script>

<style scoped>

</style>