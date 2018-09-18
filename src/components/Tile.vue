<template>
    <div class="tile">
        <label for="new-thought">Box Text:</label>
        <input v-model="thought.text" type="text" id="new-thought">
        <div>{{ thought.text }}</div>
    </div>
</template>

<script lang="ts">
    import Vue from "vue";

    export default Vue.extend({
        props: {
            thought: {
                type: Object,
                required: true
            }
        }
    })
</script>

<style>
.tile {
    margin: 0px;
    border: solid royalblue 5px;
    justify-self: stretch;
    align-self: stretch;
}
</style>
