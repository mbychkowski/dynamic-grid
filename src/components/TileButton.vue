<template>
    <div>
        <button v-on:click="onClick" class="click" v-bind:class="[ location, direction ]"></button>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue';

    export default Vue.extend({
        props: {
            onClick: {
                type: Function,
                required: true
            },

            location: {
                type: String,
                required: true
            },

            direction: {
                type: String,
                required: true
            }
        }
    });

</script>

<style>

button:focus {
    outline: 0;
}

.click {
    position: fixed;
    border-radius: 20px;
    background: #ff049f;
    transition: all 0.5s ease;
}

.horzDir {
    top: 25vh;
    height: 50vh; width: 64px;
}

.vertDir {
    left: 25vw;
    height: 64px; width: 50vw;
}

.leftClick {
    left: -52px;
}
.leftClick:hover {
    left: -20px;
}

.topClick {
    top: -52px;
}
.topClick:hover {
    top: -20px;
}

.bottomClick {
    bottom: -52px;
}
.bottomClick:hover {
    bottom: -20px;
}

.rightClick {
    right: -52px;
}
.rightClick:hover {
    right: -20px;
}

</style>
