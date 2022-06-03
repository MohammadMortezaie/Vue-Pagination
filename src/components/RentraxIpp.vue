<template>
    <select class="form-select" v-model="ipp" @click="changePage">
        <template v-for="item in items" :key="item.id" >
            <option v-bind:if="(item == ipp) ? 'selected' : ''"  >
                {{ item.name }}
            </option>
        </template>
    </select>

</template>

<script>
export default {
    data() {
        return {
            items: [
                { id: 1, name: '5' },
                { id: 2, name: '10' },
                { id: 3, name: '15' },
                { id: 4, name: '20' }
            ],
            ipp: 5
        }
    },
    methods: {
        changePage() {
            this.$emit("changeIpp", this.ipp);
        },
    },
    emits: ["changeIpp"],
};
</script>
