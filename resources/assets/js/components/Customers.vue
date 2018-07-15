<template>
    <table class="table table-bordered">
            <thead>
            <tr>
                <th>Name</th>
                <th>Email</th>
            </tr>
            </thead>
            <tbody>
                <tr v-for = "customer in customers">
                    <td>{{customer.name}}</td>
                    <td>{{customer.email}}</td>
                </tr>
            </tbody>
    </table>
</template>

<script>

    export default {

        data() {
            return {
                customers: [],
            }
        },



        created () {
            this.fetchCustomer();
        },

        methods:{
            fetchCustomer(){
                 this.$http.get('customer').then(response  => { this.customers = response.data.customers});
            }
        }
    }
</script>
