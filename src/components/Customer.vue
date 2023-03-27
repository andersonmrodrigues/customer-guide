<template>
    <div :class="{ 'customer': !isPremium, 'customer-premium': isPremium }">
        <h4>Name: {{ customer.name }}</h4>
        <hr>
        <p>E-mail: {{ customer.email | emailProcess }}</p>
        <p v-if="showAge">Age: {{ customer.age }}</p>
        <p v-else>User choose not show his age</p>
        <button @click="changeColor($event)">Change Color</button>
        <button @click="eventDelete()">Delete</button>
        <h4>Custom ID: {{ customId }}</h4>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isPremium: false
        }
    },
    props: {
        customer: Object,
        showAge: Boolean
    },
    methods: {
        changeColor: function ($event) {
            console.log($event)
            this.isPremium = !this.isPremium
        },
        eventDelete: function () {
            this.$emit("deleteMe", {
                component: this,
                id: this.customer.id,
            });
        },
        test: function () {
            alert('teste');
        }
    },
    filters: {
        emailProcess: function (value) {
            return value.toUpperCase();
        }
    },
    computed: {
        customId: function () {
            return (this.customer.email + this.customer.name + this.customer.id).toUpperCase();
        }
    }
}
</script>


<style scoped>
.customer {
    background-color: antiquewhite;
    padding: 1%;
    margin-bottom: 1%;
}

.customer-premium {
    background-color: rgb(114, 114, 114);
    color: gold;
    padding: 1%;
    margin-bottom: 1%;
}
</style>