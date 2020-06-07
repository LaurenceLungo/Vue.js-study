<template>
    <div class="done-item">
        <p>
            {{done.title}}
            <button @click="$emit('del-done', done.id)" class="del">x</button>
        </p>
    </div>
</template>

<script>
export default {
    name: "DoneItem",
    props: ["done"]
}
</script>

<style scoped>
    .done-item {
        background: #f4f4f4;
        padding: 10px;
        border-bottom: 1px #ccc dotted;
    }

    .del {
        background: #ff0000;
        color: #ffff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float: right;
    }
</style>