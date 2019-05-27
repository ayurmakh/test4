<template>
    <div class="wrapper">   
        <div class="chars top">
            <span v-for="char in alphabet" :key="char">{{char}}</span>
        </div> 
        <div class="chars bottom">
            <span v-for="char in alphabet" :key="char">{{char}}</span>
        </div>
        <div class="nums left">
            <span v-for="num in nums" :key="num">{{num}}</span>
        </div>
        <div class="nums right">
            <span v-for="num in nums" :key="num">{{num}}</span>
        </div> 
        <div class="field">
            <div v-for="x in 8" :key="x" :class="['rows']">
                <div v-for="y in 8" :key="y" 
                    :class="['cell', {
                        'black': isBlack(x, y), 
                        'blue': isTargetCell(x - 1, y - 1),
                        'green': isWay(x - 1, y - 1)
                    }]" 
                    @click="findWays(x - 1, y - 1)"></div>
            </div>
        </div>
        
    </div>
</template>

<script>
export default {
    data() {
        return {
            alphabet: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H'],
            nums: [8, 7, 6, 5, 4, 3, 2, 1],
            targetCell: {
                x: 0,
                y: 0
            },
            ways: []
        }
    },
    name: 'Chess',
    methods: {
        isBlack(x, y) {
        if (((x % 2 != 0) && (y % 2 == 0)) || ((x % 2 == 0) && (y % 2 != 0)))
            return true;
        },
        findWays(x, y) { 
            this.targetCell.x = x;
            this.targetCell.y = y;
            this.ways = [];
            for (let i = 0; i < 8; i++) 
                for (let j = 0; j < 8; j++) 
                    if (
                            ((i == x - 2) && ((j == y - 1) || (j == y + 1))) ||
                            ((i == x - 1) && ((j == y - 2) || (j == y + 2))) ||
                            ((i == x + 1) && ((j == y - 2) || (j == y + 2))) ||
                            ((i == x + 2) && ((j == y - 1) || (j == y + 1))))	
                        this.ways.push({x: i, y: j});                        
        },
        isTargetCell(x, y) {
            if ((x == this.targetCell.x) && (y == this.targetCell.y))
                return true;
        },
        isWay(x, y) {
            for (let i = 0; i < this.ways.length; i++)
                if ((this.ways[i].x == x) && (this.ways[i].y == y))
                    return true;
        }
    }
}
</script>

<style lang="scss">
    .wrapper {
        width: 520px;
        height: 520px;
        margin: 0 auto;
        border: 1px solid gray;
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
    }

    .field {
        width: 450px;
        height: 450px;
        display: grid;
        grid-template-rows: repeat(8, 1fr);
    }

    .rows {
        display: grid;
        grid-template-columns: repeat(8, 1fr);
    }

    .cell {
        border: 1px solid gray
    }

    .black {
        background-color: black;
        border: none;
    }

    .blue {
        background-color: blue;
        border: none;
    }

    .green {
        background-color: green;
        border: none;
    }

    * {
        font-family: sans-serif;
        color: gray;
    }

    .coordinates {
        position: absolute;
    }

    .top {
        top: 0;
        padding-top: 10px;
    }

    .bottom {
        bottom: 0;
        padding-bottom: 7px;
    }

    .chars {
        position: absolute;
        width: 450px;
        display: flex;
        justify-content: space-around;
    }

    .nums {
        position: absolute;
        display: flex;
        height: 450px;
        flex-direction: column;
        justify-content: space-around;
    }

    .left {
        left: 0;
        padding-left: 13px;
    }

    .right {
        right: 0;
        padding-right: 13px;
    }
</style>
