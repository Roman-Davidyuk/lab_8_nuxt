<template>
    <div>
        <title>Products List</title>
        <div
            class="flex px-3 py-3.5 border-b border-gray-200 dark:border-gray-700"
        >
            <USelectMenu
                v-model="selectedColumns"
                :options="columns"
                multiple
                placeholder="Колонки"
            />
        </div>

        <div
            class="flex px-3 py-3.5 border-b border-gray-200 dark:border-gray-700"
        >
            <UInput v-model="q" placeholder="Фільтр" />
        </div>
        <UTable
            :columns="selectedColumns"
            v-model="selected"
            :rows="rows"
            v-model:sort="sort"
            sort-mode="manual"
        >
            <template #rating-data="{ row }">
                <span :style="{ color: row.rating > 4.5 ? 'green' : 'red' }">
                    {{ row.rating }}
                </span>
            </template>
            <template #thumbnail-data="{ row }">
                <img
                    class="w-[100px] h-[100px]"
                    :src="row.thumbnail"
                    alt="Thumbnail"
                />
            </template>
        </UTable>
        <div
            class="flex justify-end px-3 py-3.5 border-t border-gray-200 dark:border-gray-700"
        >
            <UPagination
                v-model="page"
                :page-count="pageCount"
                :total="filteredPeople.length"
            />
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

const { pending, data } = await useLazyAsyncData<any>(
    "products",
    () => $fetch("https://dummyjson.com/products") as any
);

const products = data.value.products;

const columns = [
    {
        key: "id",
        label: "ID",
        sortable: true,
    },
    {
        key: "title",
        label: "Title",
        sortable: true,
    },
    {
        key: "description",
        label: "Description",
        sortable: true,
    },
    {
        key: "rating",
        label: "Rating",
        sortable: true,
    },
    {
        key: "price",
        label: "Price",
        sortable: true,
    },
    {
        key: "brand",
        label: "Brand",
        sortable: true,
    },
    {
        key: "category",
        label: "Category",
        sortable: true,
    },
    {
        key: "thumbnail",
        label: "Thumbnail",
    },
];

const selectedColumns = ref([...columns]);

const selected = ref([products[1]]);
const q = ref("");
const page = ref(1);
const pageCount = 5;

const sort = ref({ column: "title", direction: "asc" as const });

const sortedRows = computed(() => {
    const sortedProducts = [...products];
    const { column, direction } = sort.value;

    if (column && direction) {
        sortedProducts.sort((a, b) => {
            const aValue = a[column];
            const bValue = b[column];
            if (aValue < bValue) return direction === "asc" ? -1 : 1;
            if (aValue > bValue) return direction === "asc" ? 1 : -1;
            return 0;
        });
    }

    return sortedProducts;
});

const filteredPeople = computed(() => {
    if (!q.value) {
        return sortedRows.value;
    }
    page.value = 1;
    return sortedRows.value.filter((product) => {
        return Object.values(product).some((value) => {
            return String(value).toLowerCase().includes(q.value.toLowerCase());
        });
    });
});

const rows = computed(() => {
    return filteredPeople.value.slice(
        (page.value - 1) * pageCount,
        page.value * pageCount
    );
});
</script>
