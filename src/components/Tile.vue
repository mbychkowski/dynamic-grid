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
    border: solid #2c3e50 1px;
    border-radius: 3px;
    box-shadow: 0px 4px 8px 0px rgba(44, 62, 80, 0.10), 0px 6px 20px 0px rgba(44, 62, 80, 0.09);
    justify-self: stretch;
    align-self: stretch;
}
</style>
