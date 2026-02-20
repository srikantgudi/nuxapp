<template>
    <div>
        <div class="text-3xl pb-2 border-b-2">Products</div>
        <div class="shadow-lg shadow-gray-400" style="height:80vh;overflow-y: auto;">
            <table class="w-full">
                <thead class="bg-gray-800 text-gray-200 sticky top-0">
                    <tr>
                        <td class="p-1 w-20 text-right">Id</td>
                        <td class="p-1 w-100">Name</td>
                        <td class="p-1 w-80">Qty/Unit</td>
                        <td class="p-1 text-right">Unit price</td>
                        <td class="p-1 text-right">Reorder level</td>
                    </tr>
                </thead>
                <tbody>
                    <tr class="align-top even:bg-gray-200" v-for="p in products.value" :key="p.productId">
                        <td class="p-1 text-right">{{p.productId}}</td>
                        <td class="p-1">{{p.productName}}</td>
                        <td class="p-1">{{p.qtyPerUnit}}</td>
                        <td class="p-1 text-right">{{p.unitPrice.toFixed(2)}}</td>
                        <td class="p-1 text-right">{{p.rorLevel}}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script setup>
    import {ref, reactive, onMounted} from 'vue';
    const products = reactive([])

    onMounted(async () => {
        const resp = await fetch('http://localhost:9000/products');
        const data = await resp.json();
        products.value = data.products;
    })
</script>