<template>
    <div>
        <RouterLink :to="'/finishingDetail/' + finishing.id">
            <button class="btn btn-warning" type="button">Manage</button>
        </RouterLink>
 
    </div>
</template>

<script>
export default {
    name: 'BtnChange',
    props: ['finishing'],
    
    

}

</script>

