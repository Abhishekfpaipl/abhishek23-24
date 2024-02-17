<template>
    <div>
        <RouterLink :to="'/ProductionPage/' + production.id">
            <button class="btn btn-warning" type="button">Manage</button>
        </RouterLink>
 
    </div>
</template>

<script>
export default {
    name: 'BtnChange',
    props: ['production'],
    
    

}

</script>

<style scoped>
table th:nth-child(1),

.table td:nth-child(1) {
    position: sticky;
    left: 0;
    background-color: #e8e8e8;
    color: #373737;
    z-index: 10;
}

.accordion-button:not(.collapsed) {
    color: #fff;
    background-color: none;

}

.accordion {
    --bs-accordion-active-bg: #606C5D !important;
    --bs-accordion-btn-focus-box-shadow: none;
    --bs-accordion-active-color: #ffffff;
    --bs-accordion-btn-icon-width: 1rem;

}

.accordion-item {
    border: none;

}

.nav-link.active {
    color: #fff;
    background-color: #606C5D;
}

.nav-link {
    color: #000000;
}
</style>