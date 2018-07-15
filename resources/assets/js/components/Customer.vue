<template>
    <tr>
        <td>{{customer.name}}</td>
        <td>{{customer.email}}</td>
        <td>
            <button type="button" v-on:click = "$emit('delete-customer', customer)" class="btn btn-danger btn-xs">Delete</button>
        </td>
    </tr>
</template>

<script>
    export default {
        props: ['customer']
    }
</script>