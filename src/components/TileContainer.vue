<template>
    <div>
        <button @click="removeTileHorz">LEFT</button>
        <button @click="removeTileVert">TOP</button>
        <button @click="addTileVert">BOTTOM</button>
        <button @click="addTileHorz">RIGHT</button>
        <div id="container">
            <Tile
                v-for="thought in thoughts"
                :key="thought.id" 
                :thought="thought" />
        </div>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue';
    import Tile from './Tile.vue';

    let nextID = 1;

    export default Vue.extend({
        components: {
            Tile
        },
        data() {
            return {
                thoughts: [
                    {
                        id: nextID++,
                        text: 'ONE'
                    }
                ]
            }
        },
        methods: {
            addTileVert: function(text: string) {

                let gridState = this.getGridState();

                // Why is this needed?
                console.log(gridState.row.num, gridState.row.num++);

                let rowString: string = (gridState.row.num++).toString();

                this.setGridState(rowString, gridState.col.string);

                for (var i = 0; i < gridState.col.num; i++) {
                    let newThought = 
                    {
                        id: nextID++,
                        text: nextID.toString()
                    }

                    this.thoughts.push(newThought);
                }

            },
            addTileHorz: function(text: string) {

                let gridState = this.getGridState();

                // Why is this needed?
                console.log(gridState.col.num, gridState.col.num++);

                let colString: string = (gridState.col.num++).toString();

                this.setGridState(gridState.row.string, colString);

                for (var i = 0; i < gridState.row.num; i++) {
                    let newThought = 
                    {
                        id: nextID++,
                        text: nextID.toString()
                    }

                    this.thoughts.push(newThought);
                }

            },
            removeTileVert: function(text: string) {

                let gridState = this.getGridState();

                // Why is this needed?
                console.log(gridState.row.num, gridState.row.num--);

                let rowString: string = (gridState.row.num--).toString();

                this.setGridState(rowString, gridState.col.string);

                for (var i = 0; i < gridState.col.num; i++) {

                    this.thoughts.pop();
                }

            },
            removeTileHorz: function(text: string) {

                let gridState = this.getGridState();

                // Why is this needed?
                console.log(gridState.col.num, gridState.col.num--);

                let colString: string = (gridState.col.num--).toString();

                this.setGridState(gridState.row.string, colString);

                for (var i = 0; i < gridState.row.num; i++) {

                    this.thoughts.pop();
                }

            },
            getGridState: function() {
                let containerEl = document.getElementById('container');
                let getRowString: string = window.getComputedStyle(containerEl).getPropertyValue('--rowNum');
                let getColString: string = window.getComputedStyle(containerEl).getPropertyValue('--colNum');

                let getRowNum: number = parseInt(getRowString);
                let getColNum: number = parseInt(getColString);

                let grid = {
                    row: 
                    {
                        string: getRowString,
                        num: getRowNum
                    },
                    col: 
                    {
                        string: getColString,
                        num: getColNum
                    } 
                }

                return grid;
            },
            setGridState: function(row: string, col: string) {
                document.documentElement.style.setProperty('--rowNum', row);
                document.documentElement.style.setProperty('--colNum', col);
            }
        }
        
    });
</script>

<style>
:root {
    --rowNum: 1;
    --colNum: 1;
}

#container {
    padding: 0; margin: 0;
    display: grid;
    height: 97vh;
    grid-template-columns: repeat(var(--colNum), 1fr);
    grid-template-rows: repeat(var(--rowNum), 1fr);
    grid-row-gap: 12px;
    grid-column-gap: 12px;
}

button {
    position: fixed;
    top: 100px;
    left: 100px;
    background: yellowgreen;
}
</style>

