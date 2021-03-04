<template>
    <div class="container text-white p-4 history">
        <h2>History</h2>
        <br>
        <div>
            <b-list-group>
                <b-list-group-item v-for="(item, index) of arrayLoaded" :key="item.id" class="text-dark listas">
                    {{ item.num1 }}
                    {{ item.simbol }}
                    {{ item.num2 }}
                    =
                    {{ item.total }}
                    <div class="buttons">
                        <button class="btn btn-outline-danger" @click="deleteHistory(index)">Delete</button>
                        <button class="btn btn-outline-success" @click="returnResult(index)">return</button>
                    </div>
                </b-list-group-item>
            </b-list-group>
        </div>
    </div>
</template>

<script>
export default {
    name: 'History',
    props: {
        arrayLoaded: Array,
        enviarAlert: undefined,
        localStorageFunction: undefined
    },
    methods: {
        deleteHistory(index) {
            this.arrayLoaded.splice(index, 1);
            this.localStorageFunction();
        },
        returnResult (index) {
            this.$emit('returnResult', this.arrayLoaded[index].total);
            this.enviarAlert();
        }
    },
    
}
</script>

<style scoped lang="scss">
    @import '@/styles/stylesHistory.scss';
</style>