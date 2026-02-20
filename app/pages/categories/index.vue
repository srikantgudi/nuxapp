<template>
    <div class="shadow-lg shadow-gray-400">
        <div class="grid grid-cols-12 gap-4">
            <div class="col-span-5">
                <div class="text-3xl pb-2 border-b-2">Categories</div>
                <div style="height:80vh;overflow-y: auto;">
                    <table class="w-full">
                        <thead class="bg-gray-800 text-gray-200 sticky top-0">
                            <tr>
                                <td class="p-1 w-10 text-right">Id</td>
                                <td class="p-1 w-40">Name</td>
                                <td class="p-1 w-auto">Description</td>
                            </tr>
                        </thead>
                        <tbody>
                            <tr @click="getproducts(c.categoryId)" class="align-top even:bg-gray-200" v-for="c in categories.value" :key="c.categoryId">
                                <td class="p-1 text-right">{{c.categoryId}}</td>
                                <td class="p-1">{{c.categoryName}}</td>
                                <td class="p-1">{{c.description}}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            <div class="col-span-7">
                <div class="text-3xl mb-2">Products</div>
                <div>
                    <table class="w-full">
                        <thead class="bg-gray-800 text-gray-200 sticky top-0">
                            <tr>
                                <td class="p-1 w-120">Product name</td>
                                <td class="p-1">Quantity per unit</td>
                                <td class="p-1 w-30 text-right">Unit price</td>
                                <td class="p-1 w-30 text-right">Reorder level</td>
                            </tr>
                        </thead>
                        <tbody>
                            <tr class="even:bg-gray-200" v-for="p in products.value" :key="p.productId">
                                <td class="p-1">{{p.productName}}</td>
                                <td class="p-1">{{p.qtyPerUnit}}</td>
                                <td class="p-1 text-right">{{p.unitPrice.toFixed(2)}}</td>
                                <td class="p-1 text-right">{{p.rorLevel}}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
    import {ref, reactive, onMounted} from 'vue';
    const categories = reactive([])
    const products = reactive([])

    onMounted(async () => {
        const resp = await fetch('http://localhost:9000/categories');
        const data = await resp.json();
        categories.value = data.categories;
    })
    const getproducts = async (catid) => {
    const resp = await fetch(`http://localhost:9000/category/${catid}/products`);
        const data = await resp.json();
        products.value = data.products;
    }
</script>