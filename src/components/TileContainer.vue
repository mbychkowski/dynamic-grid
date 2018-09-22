<template>
    <div>
        <TileButton
            v-bind:onClick="removeTileHorz" 
            v-bind:location="buttons[0].location" 
            v-bind:direction="buttons[0].direction" />
        <TileButton
            v-bind:onClick="addTileHorz" 
            v-bind:location="buttons[1].location" 
            v-bind:direction="buttons[1].direction" />
        <TileButton
            v-bind:onClick="removeTileVert" 
            v-bind:location="buttons[2].location" 
            v-bind:direction="buttons[2].direction" />
        <TileButton
            v-bind:onClick="addTileVert" 
            v-bind:location="buttons[3].location" 
            v-bind:direction="buttons[3].direction" />

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
    import TileButton from './TileButton.vue';

    let nextID = 1;

    export default Vue.extend({
        components: {
            Tile,
            TileButton
        },
        data() {
            return {
                thoughts: [
                    {
                        id: nextID++,
                        text: 'ONE'
                    }
                ],
                buttons: [
                    { direction: 'horzDir', location: 'leftClick'   },
                    { direction: 'horzDir', location: 'rightClick'  },
                    { direction: 'vertDir', location: 'topClick'    },
                    { direction: 'vertDir', location: 'bottomClick' }, 
                ]
            }
        },
         methods: {
            action: function(location: string ){

                let action;

                if(location == 'leftClick') {
                    action = this.removeTileHorz();
                } else if(location == 'rightClick') {
                    action = this.addTileHorz();
                } else if(location == 'topClick') {
                    action = this.removeTileVert();
                } else {
                    action = this.addTileVert();
                }

                return action;

                
            },
            
            addTileVert: function() {
            
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
    
            addTileHorz: function() {
            
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
    
            removeTileVert: function() {
            
                let gridState = this.getGridState();
    
                // Why is this needed?
                console.log(gridState.row.num, gridState.row.num--);
    
                let rowString: string = (gridState.row.num--).toString();
    
                this.setGridState(rowString, gridState.col.string);
    
                for (var i = 0; i < gridState.col.num; i++) {
                    this.thoughts.pop();
                }
            },
    
            removeTileHorz: function() {
            
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
    height: 98vh;
    grid-template-columns: repeat(var(--colNum), 1fr);
    grid-template-rows: repeat(var(--rowNum), 1fr);
    grid-row-gap: 14px;
    grid-column-gap: 14px;
}

button:focus {
    outline: 0;
}

</style>

