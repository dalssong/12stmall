<template>

    <v-data-table
        :headers="headers"
        :items="productSearch"
        :items-per-page="5"
        class="elevation-1"
    ></v-data-table>

</template>

<script>
    const axios = require('axios').default;

    export default {
        name: 'ProductSearchView',
        props: {
            value: Object,
            editMode: Boolean,
            isNew: Boolean
        },
        data: () => ({
            headers: [
                { text: "id", value: "id" },
                { text: "id", value: "id" },
                { text: "customerId", value: "customerId" },
                { text: "productId", value: "productId" },
            ],
            productSearch : [],
        }),
          async created() {
            var temp = await axios.get(axios.fixUrl('/productSearches'))

            temp.data._embedded.productSearches.map(obj => obj.id=obj._links.self.href.split("/")[obj._links.self.href.split("/").length - 1])

            this.productSearch = temp.data._embedded.productSearches;
        },
        methods: {
        }
    }
</script>

