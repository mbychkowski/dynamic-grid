<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <TileContainer />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src
import TileContainer from '@/components/TileContainer.vue';

@Component({
  components: {
    TileContainer
  },
})
export default class Home extends Vue {}
</script>
