<template>
    <li class="page-item" v-bind:class="this.page === i ? 'active' : ''" v-for="i in range(start,end)" :key="i">
        <a href="#" @click="changePage(i)" class="page-link">{{ i }}</a>
    </li>
</template>

<script>
export default {
    props: {
        page: Number,
        start: Number,
        end: Number,
    },
    methods: {
        range: function(min,max){
            var array = [],
            j = 0;
            for(var i = min; i <= max; i++){
                array[j] = i;
                j++;
            }
            return array;
        },
        changePage(pageNumber){
            this.$emit('changePage',pageNumber);
        }
    },
    emits: ["changePage"],
};
</script>
