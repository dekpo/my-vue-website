<script>
export default {
    data() {
        return {
            count: 1,
            id: this.$route.params.id,
            myApi: {},
            myPicsum: {}
        }
    },
    methods: {
        increment() {
            this.count++
        },
        loadItem() {
            fetch('http://127.0.0.1:8000/api/picture/' + this.id)
                .then(res => res.json())
                .then(data => {
                    this.myApi = data;
                })
        },
        loadSinglePicsum() {
            fetch('https://picsum.photos/id/' + this.id + '/info')
                .then(res => res.json())
                .then(data => {
                    this.myPicsum = data
                })
        }
    },
    mounted() {
        this.loadItem();
        this.loadSinglePicsum();
    },
    updated() {
        console.log("Le composant est mis à jour:", this.count)
    }
}
</script>

<template>
    <h1>Detail page avec l'id:{{ id }}</h1>
    <h2>Count ? {{ count }}</h2>
    <h3>{{myApi?.author}}</h3>
    <h3>{{myPicsum?.author}}</h3>
    <button @click="increment">Click</button>
</template>

<style>
</style>