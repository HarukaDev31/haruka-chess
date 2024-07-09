<template>
    <div class="table-grid">
        <img v-if="piece" :src="piece.url" class="piece-img" />
    </div>
</template>
<script setup>
const props = defineProps(['piece']);

</script>
<style scoped>
.piece-img {
    width: 100%;
    height: 100%;
}

.piece-img:hover {
    cursor: pointer;

}

.table-row:nth-child(odd) .table-cell:nth-child(even) .piece-img:hover {
    -webkit-filter: drop-shadow(2px 1px 0 black) drop-shadow(-1px -1px 0 black);
    filter: drop-shadow(2px 1px 0 black) drop-shadow(-1px -1px 0 black);
}

.table-row:nth-child(even) .table-cell:nth-child(odd) .piece-img:hover {
    -webkit-filter: drop-shadow(2px 1px 0 black) drop-shadow(-1px -1px 0 black);
    filter: drop-shadow(2px 1px 0 black) drop-shadow(-1px -1px 0 black);
}

.table-row:nth-child(odd) .table-cell:nth-child(odd) .piece-img:hover {
    -webkit-filter: drop-shadow(2px 1px 0 white) drop-shadow(-1px -1px 0 white);
    filter: drop-shadow(2px 1px 0 white) drop-shadow(-1px -1px 0 white);
}

.table-row:nth-child(even) .table-cell:nth-child(even) .piece-img:hover {
    -webkit-filter: drop-shadow(2px 1px 0 white) drop-shadow(-1px -1px 0 white);
    filter: drop-shadow(2px 1px 0 white) drop-shadow(-1px -1px 0 white);
}
</style>