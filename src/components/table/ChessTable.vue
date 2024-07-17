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
    const pawnRows = {
        2: { name: 'pawn', url: '/src/assets/chess-pieces/bpawn.png' },
        7: { name: 'pawn', url: '/src/assets/chess-pieces/wpawn.png' },
    };

    const mainRows = {
        1: {
            1: { name: 'rook', url: '/src/assets/chess-pieces/brook.png' },
            8: { name: 'rook', url: '/src/assets/chess-pieces/brook.png' },
            2: { name: 'knight', url: '/src/assets/chess-pieces/bhorse.png' },
            7: { name: 'knight', url: '/src/assets/chess-pieces/bhorse.png' },
            3: { name: 'bishop', url: '/src/assets/chess-pieces/bbishop.png' },
            6: { name: 'bishop', url: '/src/assets/chess-pieces/bbishop.png' },
            4: { name: 'queen', url: '/src/assets/chess-pieces/bqueen.png' },
            5: { name: 'king', url: '/src/assets/chess-pieces/bking.png' },
        },
        8: {
            1: { name: 'rook', url: '/src/assets/chess-pieces/wrook.png' },
            8: { name: 'rook', url: '/src/assets/chess-pieces/wrook.png' },
            2: { name: 'knight', url: '/src/assets/chess-pieces/whorse.png' },
            7: { name: 'knight', url: '/src/assets/chess-pieces/whorse.png' },
            3: { name: 'bishop', url: '/src/assets/chess-pieces/wbishop.png' },
            6: { name: 'bishop', url: '/src/assets/chess-pieces/wbishop.png' },
            4: { name: 'queen', url: '/src/assets/chess-pieces/wqueen.png' },
            5: { name: 'king', url: '/src/assets/chess-pieces/wking.png' },
        }
    };

    if (pawnRows[row]) {
        return pawnRows[row];
    }

    return mainRows[row] ? mainRows[row][col] : undefined;
};

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