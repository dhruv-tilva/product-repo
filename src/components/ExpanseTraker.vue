<template>
    <div class="max-w-sm mx-auto lg:max-w-[50rem]">
        <h1 class="p-4 text-3xl font-semibold sm:text-4xl lg:text-5xl">Expanse Traker</h1>
        <form v-on:submit.prevent="addItem" action=""
            class="w-full p-4 flex flex-col gap-y-2 lg:flex-row lg:gap-y-0 lg:gap-x-3">
            <input
                class="px-7 py-3 text-lg font-medium outline-none bg-[#ffd5d5] placeholder-gray-400 border-b-2 border-transparent focus:border-[#ff2947] lg:w-full"
                type="text" placeholder="Description" v-model="newItems.name" required>
            <input
                class="px-7 py-3 text-lg font-medium outline-none bg-[#ffd5d5] border-b-2 border-transparent focus:border-[#ff2947] lg:w-[28%]"
                type="number" placeholder="Amount" v-model="newItems.price" required min="1" ref="amt">
            <button type="submit"
                class="w-full bg-[#ff2947] py-3 text-lg font-medium text-white lg:w-[21%] transition-all duration-200 hover:bg-[#e71533]">Add</button>
        </form>
    </div>

    <div class="max-w-xl mx-auto p-4 lg:max-w-[50rem]">
        <table class="w-full border-collapse">
            <tr>
                <th class="border-2 border-[#dddddd] p-2 text-left lg:w-[44%]">Description</th>
                <th class="border-2 border-[#dddddd] p-2 text-left lg:w-[14%]">Amount</th>
                <th class="border-2 border-[#dddddd] p-2 text-left">Date</th>
            </tr>
            <tr v-for="(x, ind) in items" :key="ind">
                <td>{{ x.name }}</td>
                <td>{{ x.price }} <span>&#8377</span></td>
                <td class="">{{ hour + " : " }}{{ minutes + ", " }}{{ day + " " }}{{ Da + " " }}{{ month + " " }}{{
                    date.getFullYear() }}</td>
            </tr>
        </table>
        <p class="text-xl font-bold text-right mt-5">Total Expanse : {{ total }} &#8377</p>
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
            },
            total: 0,
            date: new Date(),
        }
    },
    methods: {
        addItem: function () {
            let value = this.newItems;
            value.name = value.name.charAt(0).toUpperCase() + value.name.slice(1)
            if (value.name && value.price && value.price > 0) {
                this.items.push(value);
                this.total += this.items[this.items.length - 1].price;
                // this.totals.push(this.total)
                // console.log(this.total)
                // localStorage.setItem(value.name, value.price
                this.newItems = {
                    name: "",
                    price: ""
                }
                this.toLocalStorage();
            }
        },
        toLocalStorage() {
            localStorage.setItem("item", JSON.stringify(this.items))
            localStorage.setItem("full", JSON.stringify(this.total))
        },
        fetchLocalStorage() {
            const saveData = localStorage.getItem("item");
            if (saveData) {
                this.items = JSON.parse(saveData);
            }
            const saveTotal = localStorage.getItem("full")
            if (saveTotal) {
                this.total = saveTotal;
            }
        }
    },
    mounted() {
        this.fetchLocalStorage();
    },
    computed: {
        hour() {
            if (this.date.getHours() < 10) {
                return "0" + this.date.getHours();
            } else {
                return this.date.getHours();
            }
        },
        minutes() {
            if (this.date.getMinutes() < 10) {
                return "0" + this.date.getMinutes();
            } else {
                return this.date.getMinutes();
            }
        },
        day() {
            switch (this.date.getDay()) {
                case 0:
                    return "Sun";
                    break;
                case 1:
                    return "Mon";
                    break;
                case 2:
                    return "Tue";
                    break;
                case 3:
                    return "Wed";
                    break;
                case 4:
                    return "Thu";
                    break;
                case 5:
                    return "Fri";
                    break;
                case 6:
                    return "Sat";
            }
        },
        Da() {
            if (this.date.getDate() < 10) {
                return "0" + this.date.getDate();
            } else {
                return this.date.getDate();
            }
        },
        month() {
            switch (this.date.getMonth()) {
                case 0:
                    return "Jan";
                    break;
                case 1:
                    return "Feb";
                    break;
                case 2:
                    return "Mar";
                    break;
                case 3:
                    return "Apr";
                    break;
                case 4:
                    return "May";
                    break;
                case 5:
                    return "Jun";
                    break;
                case 6:
                    return "July";
                    break;
                case 7:
                    return "Aug";
                    break;
                case 8:
                    return "Sept";
                    break;
                case 9:
                    return "Oct";
                    break;
                case 10:
                    return "Nov";
                    break;
                case 11:
                    return "Dec";
            }
        }
    }
}
</script>

<style>
tr:nth-child(even) {
    background-color: #ffd5d5;
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
