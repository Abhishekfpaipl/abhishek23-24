<template>
    <div>
        <RouterLink :to="'/subfabDetail/' + subfab.id">
        <button class="btn btn-warning" type="button">Manage</button>
        </RouterLink>

    </div>
</template>

<script>
export default {
    name: 'BtnChange',
    props: ['subfab'],

}

</script>


