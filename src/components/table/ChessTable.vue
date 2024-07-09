<template>
    <section id="chess-table">
        <div v-for="(row, rowIndex) in tableChess" :key="rowIndex" class="table-row">
            <TableGrid v-for="(col, colIndex) in row" :key="colIndex" :piece="getCellPiece(rowIndex + 1, colIndex + 1)"
                class="table-cell" :style="getCellStyle(rowIndex + 1, colIndex + 1, tableChess.length, row.length)" />
        </div>
    </section>
</template>
<script setup>
import { ref } from 'vue'
import TableGrid from './TableGrid.vue';
const tableChess = ref([]);
const initTable = (row, col) => {
    for (let i = 0; i < row; i++) {
        tableChess.value.push([]);
        for (let j = 0; j < col; j++) {
            tableChess.value[i].push(0);
        }
    }
}
const getCellPiece = (row, col) => {
    if (row == 2) {
        return {
            name: 'pawn',
            url: '/src/assets/chess-pieces/bpawn.png'
        }
    } else if (row == 7) {
        return {
            name: 'pawn',
            url: '/src/assets/chess-pieces/wpawn.png'
        }
    } else if (row == 1 || row == 8) {
        if (col == 1 || col == 8) {
            return {
                name: 'rook',
                url: row == 1 ? '/src/assets/chess-pieces/brook.png' : '/src/assets/chess-pieces/wrook.png'
            }
        } else if (col == 2 || col == 7) {
            return {
                name: 'knight',
                url: row == 1 ? '/src/assets/chess-pieces/bhorse.png' : '/src/assets/chess-pieces/whorse.png'
            }
        } else if (col == 3 || col == 6) {
            return {
                name: 'bishop',
                url: row == 1 ? '/src/assets/chess-pieces/bbishop.png' : '/src/assets/chess-pieces/wbishop.png'
            }
        } else if (col == 4) {
            return {
                name: 'queen',
                url: row == 1 ? '/src/assets/chess-pieces/bqueen.png' : '/src/assets/chess-pieces/wqueen.png'
            }
        } else if (col == 5) {
            return {
                name: 'king',
                url: row == 1 ? '/src/assets/chess-pieces/bking.png' : '/src/assets/chess-pieces/wking.png'
            }
        }
    }
}
const getCellStyle = (row, col, rowCount, colCount) => {
    const width = `calc(
    min(80vh/${rowCount}, 80vw/${colCount})
    )`;
    const height = `calc(
    min(80vh/${rowCount}, 80vw/${colCount})
    )`;
    return {
        backgroundColor: (row + col) % 2 === 0 ? 'black' : 'white',
        width: width,
        height: height
    }
}
initTable(8, 8);
</script>
<style scoped>
.table-row {
    display: flex;
    flex-direction: row;
}
</style>