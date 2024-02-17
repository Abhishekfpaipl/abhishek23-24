<template>
    <!-- <div class="container d-flex justify-content-between align-items-center bg-light"
        style="height: 63px !important;box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;">
        <div class="">
            <h3>Fabricator</h3>
        </div>
        <div class="d-flex justify-content-between gap-2">
            <i class="bi bi-house fs-4"></i>
            <i class="bi bi-shop-window fs-4"></i>
            <i class="bi bi-gear fs-4"></i>
        </div>
    </div> -->
    <div class="px-2 d-flex justify-content-between align-items-center  border"
        style="height: 63px !important; background: #28CC9E;">
        <div class=" text-white">
            <h3>
                <slot>Order</slot>
            </h3>
        </div>
        <div data-bs-toggle="offcanvas" data-bs-target="#offcanvasExampleMenu"
            aria-controls="offcanvasExampleMenu">
            <i class="bi bi-list fs-1 text-white d-flex align-items-center"></i>
        </div>

        <!-- Menu -->
        <div class="offcanvas offcanvas-end" tabindex="-1" id="offcanvasExampleMenu" aria-labelledby="offcanvasExampleLabel"
            style="width:80vw !important">
            <div class="offcanvas-header">
                <h5 class="offcanvas-title" id="offcanvasExampleLabel">Menu</h5>
                <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
            </div>
            <div class="offcanvas-body p-0">
                <div>
                    <ul class="list-group rounded-0">
                        <router-link to="/login-page" class="text-decoration-none text-dark ">
                            <li class="list-group-item ">Login / SignUp</li>
                        </router-link>

                        <router-link to="/detail" class="text-decoration-none text-dark">
                            <li class="list-group-item border-top-0">Profile / Account</li>
                        </router-link>

                        <router-link to="/production-manager/order" class="text-decoration-none text-dark">
                            <li class="list-group-item border-top-0">Production Manager</li>
                        </router-link>

                        <router-link to="/subfab" class="text-decoration-none text-dark">
                            <li class="list-group-item border-top-0">Job Worker Incharge</li>
                        </router-link>
 
                        <!-- <router-link to="/subfab" class="text-decoration-none text-dark"> -->
                        <router-link to="/cutting" class="text-decoration-none text-dark">
                            <li class="list-group-item border-top-0">Cutting Incharge</li>
                        </router-link>

                        <router-link to="/subfab" class="text-decoration-none text-dark">
                        <!-- <router-link to="/production/order" class="text-decoration-none text-dark"> -->
                            <li class="list-group-item border-top-0">Line Incharge</li>
                        </router-link>

                        <router-link to="/subfab" class="text-decoration-none text-dark">
                        <!-- <router-link to="/finishing" class="text-decoration-none text-dark"> -->
                            <li class="list-group-item border-top-0">Finishing Incharge</li>
                        </router-link>

                        <router-link to="/users/members" class="text-decoration-none text-dark">
                            <li class="list-group-item border-top-0">Members</li>
                        </router-link>

                        <button class="btn btn-outline-primary m-2 mt-3">Log Out</button>
                    </ul>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
export default {
    name: 'TopNav',

}
</script>

<style scoped></style>