<template>
    <div>
        <RouterLink :to="'/DetailPage/' + manager.id">
            <button class="btn btn-warning" style="width: 6em;" type="button" aria-controls="offcanvasRight">Manage</button>
        </RouterLink>
 
    </div>
</template>

<script>
export default {
    name: 'BtnChange',
    props: ['manager'],
}

</script>

