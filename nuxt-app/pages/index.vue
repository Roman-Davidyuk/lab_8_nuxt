<script setup lang="ts">
const id = ref(1);

const { data, error, refresh } = await useFetch(`/api/users/${id.value}`, {
    watch: [id],
});
</script>
