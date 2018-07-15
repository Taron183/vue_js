<template>
    <tr>
        <td>
            <input type="text" v-modal="editForm.name" class="form-control" v-if="edit">
            <span v-else>{{customer.name}}</span>

        </td>
        <td>
            <input type="text" v-modal="editForm.email" class="form-control" v-if="edit">
            <span v-else>{{customer.email}}</span>
        </td>
        <td>
            <button type="button" v-on:click = "editCustomer" class="btn btn-info btn-xs" v-if="!edit">
                Edit
            </button>

            <button type="button" v-on:click = "cancelEdit" class="btn btn-default btn-xs" v-if="edit">
                Cancel
            </button>

            <button type="button" v-on:click = "updateCustomer(customer, editForm)" class="btn btn-primary btn-xs"
                    v-if = "edit">
                Update
            </button>

            <button type="button" v-on:click = "$emit('delete-customer', customer)" class="btn btn-danger btn-xs" v-if="!edit">
                Delete
            </button>
        </td>
    </tr>
</template>

<script>
    export default {
        props: ['customer'],
        data(){
            return {
                edit:false,
                editForm:{
                    name: '',
                    email: ''
                }
            }
        },

        methods:{
            editCustomer(){
                this.edit = true;
                this.editForm.name = this.customer.name;
                this.editForm.email = this.customer.email;
            },

            cancelEdit(){
                this.edit = false;
                this.editForm.name = '';
                this.editForm.email = '';
            },

            updateCustomer(oldCustomer, newCustomer){
                this.$http.patch("/customer/"+ oldCustomer.id, newCustomer).then(response => {
                    this.$emit('update-customer');
                    this.cancelEdit();

                });

            }
        }
    }
</script>