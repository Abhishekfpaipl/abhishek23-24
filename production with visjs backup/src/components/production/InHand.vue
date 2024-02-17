<template>
    <div style="padding-bottom: 80px;">
        <!-- <ProductionLinks active="Order"></ProductionLinks> -->
        <TopNav>Production</TopNav>
        <MembersPage></MembersPage>

    </div>
    <ProductionBottomnav></ProductionBottomnav>
</template>

<script>

// import ProductionLinks from './ProductionLinks.vue';
import MembersPage from '../user/MembersPage.vue';
import TopNav from '../navbar/TopNav.vue'
import ProductionBottomnav from '../navbar/ProductionBottomnav.vue';
export default {
    components: { ProductionBottomnav, TopNav, MembersPage }
}
</script>

<style  scoped>
table th:nth-child(1),

.table td:nth-child(1) {
    position: sticky;
    left: 0;
    background-color: #e8e8e8;
    color: #373737;
    /* z-index: 10; */
}

.accordion-button:not(.collapsed) {
    color: #fff;
    background-color: none;

}
</style>