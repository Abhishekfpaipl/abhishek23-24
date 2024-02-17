<template>
  <div class="home">
    <TopNav>Dashboard</TopNav>
    <div class="d-flex bg-secondary text-white justify-content-between container py-2">
      <p class="m-0">Running Catelog</p>
      <p class="m-0">View More<i class="bi bi-arrow-right "></i></p>
    </div>
  </div>
</template>

<script>

import TopNav from '@/components/navbar/TopNav.vue';
export default {
  name: "HomeView",
  components: { TopNav }
};
</script>
