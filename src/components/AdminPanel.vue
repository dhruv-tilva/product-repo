<template>
    <div class="max-w-sm mx-auto">
        <form v-on:submit.prevent="addItem" action="" class="w-full p-6 flex flex-col gap-y-2">
            <input
                class="px-7 py-3 text-lg font-medium outline-none bg-blue-50 border-b-2 border-transparent focus:border-blue-600"
                type="text" placeholder="Product Name" v-model="newItems.name">
            <input
                class="px-7 py-3 text-lg font-medium outline-none bg-blue-50 border-b-2 border-transparent focus:border-blue-600"
                type="number" placeholder="Product Price" v-model="newItems.price">
            <button type="submit" class="w-full bg-blue-400 py-3 text-lg font-medium text-white">Add Item</button>
        </form>
    </div>

    <div class="max-w-xl mx-auto">
        <table class="w-full border-collapse">
            <tr>
                <th class="border-2 border-[#dddddd] p-2 text-left">Product Name</th>
                <th class="border-2 border-[#dddddd] p-2 text-left">Price</th>
                <th class="border-2 border-[#dddddd] p-2 text-left">Remove</th>
            </tr>
            <tr v-for="(x, ind) in items" :key="ind">
                <td>{{ x.name }}</td>
                <td>{{ x.price }} <span>&#8377</span></td>
                <td class="text-center cursor-pointer text-red-600" v-on:click="deleteItem(items.indexOf(x))">Delete</td>
            </tr>
        </table>
    </div>
</template>

<script>
export default {
    data() {
        return {
            items: [],
            newItems: {
                name: "",
                price: ""
            }
        }
    },
    methods: {
        addItem: function () {
            let value = this.newItems;
            if (value.name && value.price) {
                this.items.push(value);
                localStorage.setItem(value.name, value.price)
                this.newItems = {
                    name: "",
                    price: ""
                }
            }
        },
        deleteItem: function (index) {
            this.items.splice(index, 1);
        }
    }
}
</script>

<style>
tr:nth-child(even) {
    background-color: rgb(239, 246, 255);
}

td,
th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
    font-size: 18px;
    font-weight: 500;
}
</style>
