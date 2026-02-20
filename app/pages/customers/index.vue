<template>
    <div class="shadow-md shadow-gray-400">
        <div class="grid grid-cols-12 gap-4">
            <div class="col-span-4">
                <div class="text-3xl my-2">Customers</div>
                <div style="height:70vh;overflow-y: auto;">
                    <table class="w-full">
                        <thead class="bg-gray-800 text-gray-200 sticky top-0">
                            <tr class="text-sm">
                                <td class="w-3/4">Company name</td>
                                <td>City</td>
                                <td>Country</td>
                            </tr>
                        </thead>
                        <tbody>
                            <tr @click="showorders(cu.customerId)" class="text-sm cursor-pointer even:bg-gray-300" v-for="cu in customers.value" :key="cu.customerid">
                                <td>{{cu.companyName}}</td>
                                <td>{{cu.city}}</td>
                                <td>{{cu.country}}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            <div class="col-span-8">
                <div class="grid grid-cols-12 gap-4">
                    <div class="col-span-4">
                        <div class="text-3xl mb-4">Orders</div>
                        <div v-if="orders.value">
                            <table class="w-full text-sm">
                                <thead class="bg-gray-800 text-gray-200 sticky top-0">
                                    <tr>
                                        <td class="p-1" nowrap>Order Id</td>
                                        <td class="p-1">Order date</td>
                                        <td class="p-1">Ship date</td>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr class="even:bg-gray-200" @click="showdetails(o.orderId)" v-for="o in orders.value" :key="o.orderid">
                                        <td class="p-1">{{o.orderId}}</td>
                                        <td class="p-1">{{o.orderDate}}</td>
                                        <td class="p-1">{{o.shippedDate}}</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    <div class="col-span-8">
                        <div class="text-3xl mb-4">Order details</div>
                        <div v-if="orderdetails.value">
                             <table class="w-full text-sm">
                                <thead class="bg-gray-800 text-gray-200 sticky top-0">
                                    <tr>
                                        <td class="p-1 w-2/5" nowrap>Product name</td>
                                        <td class="p-1 text-right">Quantity</td>
                                        <td class="p-1 text-right">Price</td>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr class="even:bg-gray-200" @click="showdetails(o.orderId)" v-for="od in orderdetails.value" :key="od.productName">
                                        <td class="p-1">{{od.productName}}</td>
                                        <td class="p-1 text-right">{{od.quantity}}</td>
                                        <td class="p-1 text-right">{{od.price.toFixed(2)}}</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
    import {ref, reactive, onMounted} from 'vue';

    const baseurl = 'http://localhost:9000/';
    const customers = reactive([]);
    const orders = reactive([]);
    const orderdetails = reactive([]);

    onMounted(async () => {
        const resp = await fetch(`${baseurl}customers`);
        const data = await resp.json();
        customers.value = data.customers
    })

    const showorders = async (custid) => {
        const url = `${baseurl}customer/${custid}/orders`;
        const resp = await fetch(url);
        const data = await resp.json();
        orders.value = data.orders;
        orderdetails.value = [];
    }
    const showdetails = async (orderid) => {
        const url = `${baseurl}order/${orderid}/details`;
        const resp = await fetch(url);
        const data = await resp.json();
        orderdetails.value = data.orderdetails;
    }
</script>