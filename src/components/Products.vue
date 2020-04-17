<template>
    <div>
        Products
        <hr>
        <button @click="getPrevPage">Prev</button>
        <button @click="getNextPage">Next</button>
        <ul>
            <li v-for="product in results" :key="product.id">
                {{ product.title }} - {{ product.price }}
            </li>
        </ul>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: "Products",
        data () {
            return {
                page: 1,
                results: []
            }
        },
        methods: {
            getPrevPage() {
                this.page--
                this.getPage(this.page)
            },
            getNextPage() {
                this.page++
                this.getPage(this.page)
            },
            getPage(pageNumber) {
                axios.get('http://127.0.0.1:8000/en/api/products', {
                    params: {
                        page: pageNumber
                    }
                }).then((response) => {
                    this.results = response.data.results
                })
            }
        }
    }
</script>

<style scoped>

</style>