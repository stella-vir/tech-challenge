<template>
    <div>
        <h1>
            Clients
            <a href="/clients/create" class="float-right btn btn-primary">+ New Client</a>
        </h1>

        <table class="table">
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Email</th>
                    <th>Phone</th>
                    <th>Number of Bookings</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="client in clients" :key="client.id">
                    <td>{{ client.name }}</td>
                    <td>{{ client.email }}</td>
                    <td>{{ client.phone }}</td>
                    <td>{{ client.bookings_count }}</td>
                    <td>
                        <a class="btn btn-primary btn-sm" :href="`/clients/${client.id}`">View</a>
                        <button class="btn btn-danger btn-sm" @click="deleteClient(client)">Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import axios from 'axios';


export default {
    name: 'ClientsList',

    props: ['clients'],

    data() {
        return {
            dialog: false,
        };
    },

    methods: {
        deleteClient(client) {
            if (window.confirm('Are you sure you want to delete this client?')) {
                axios.delete(`/clients/${client.id}`)
                .then(data => {
                    alert('Client deleted successfully.');
                    console.log(data);
                    window.location.reload();
                })
                .catch(error => {
                    console.log(error);
                });
            }
        }
    }
}
</script>
