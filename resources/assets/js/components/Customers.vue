
<template>
    <div>
        <form v-on:submit.prevent = "createCustomer" method="post">
            <div v-bind:class="{'form-group': true, 'has-error': errors.name}">
                <label>Name</label>
                <input type="text" v-model = "customer.name" class="form-control"/>
                <span class="help-block"  v-for="error  in errors.name" v-text="error"></span>
            </div>

            <div v-bind:class="{'form-group': true, 'has-error': errors.email}">
                <label>Email</label>
                <input type="email" v-model = "customer.email" class="form-control"/>
                <span class="help-block"  v-for="error  in errors.email" v-text="error"></span>
            </div>

            <div class="form-group">
                <input type="submit"  class="btn btn-primary" value="Create New Customer"/>
            </div>

        </form>
        <table class="table table-bordered">
            <thead>
            <tr>
                <th>Name</th>
                <th>Email</th>
            </tr>
            </thead>
            <tbody>
            <customer v-for="customer in customers"f v-bind:customer="customer"> </customer>
            </tbody>
        </table>
    </div>


</template>

<script>
    import customer from "./Customer.vue";
    export default {
        data() {
            return {
                customers: [],
                errors:[],
                customer:{
                    name: '',
                    email: '',
                }
            }
        },

        components: {customer},




        created () {
            this.fetchCustomer();
        },

        methods:{
            fetchCustomer(){
                 this.$http.get('customer').then(response  => { this.customers = response.data.customers});
            },

            createCustomer(){
                this.$http.post("/customer/",this.customer).then(response => {
                    this.customers.push(response.data.customer);
                    this.customer = {name:'', email:''}

                    if (this.errors)
                    {
                        this.errors = [];
                    }

                    console.log(response.data)
                }, response =>{
                    this.errors = response.data.errors;
                });
            }
        }
    }
</script>
