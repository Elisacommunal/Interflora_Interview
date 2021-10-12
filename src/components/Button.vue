<template>
    <button class="card--btn"><i class="fas fa-paw"></i> {{ name }} <i class="fas fa-paw"></i> </button>
</template>
<script>
export default {
    name: "Button",
    props: ['name']
}
</script>