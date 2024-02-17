<template>
    <div>
        <RouterLink :to="'/subfabDetail/' + subfab.id">
        <button class="btn btn-warning" style="width: 6em;" type="button">Manage</button>
        </RouterLink>

    </div>
</template>

<script>
export default {
    name: 'BtnChange',
    props: ['subfab'],

}

</script>


