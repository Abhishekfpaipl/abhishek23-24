<template>
    <div class="container">
        <div class=" mt-3">
            <div class="border p-2 py-3  text-white w-100 rounded-top" data-bs-toggle="collapse"
                data-bs-target="#procurement" aria-expanded="false" aria-controls="procurement"
                style="background-color: #28CC9E;">
                Fabric Procurement
            </div>
        </div>
        <div class="collapse"  id="procurement">
            <div class="">
                <div v-for="(fabric, index) in manager.fabrics" :key="index" class="">
                    <div class="border p-2 py-3  text-white w-100 rounded-top" data-bs-toggle="collapse"
                        :data-bs-target="'#fabric' + index" aria-expanded="false" :aria-controls="'fabric' + index"
                        style="background-color: #28CC9E;">
                        {{ fabric.name }} {{ fabric.fabricCode }}
                    </div>
                    <div class="collapse my-2" :id="'fabric' + index">
                        <div class="d-flex justify-content-between mb-2 px-2">
                            <p class="mb-0 fw-bold">Color</p>
                            <p class="mb-0 fw-bold">Length</p>
                            <p class="mb-0 fw-bold">Unit</p>
                        </div>
                        <div v-for="(color, colorIndex) in fabric.colors" :key="colorIndex" class="d-flex gap-3  m-2">
                            <div class="">
                                <div class="rounded-circle " style="width: 30px; height: 30px;"
                                    :style="'background-color :' + color.bg"></div>
                            </div>

                            <input type="number" class="form-control form-control-sm  text-center" v-model="color.length"
                                readonly>
                            <span>{{ color.unit }}</span>
                        </div>
                        <div class="d-flex gap-2 justify-content-center">
                            <p>Total</p>
                            <p>{{ calculateTotal(fabric.colors) }}</p>
                        </div>
                        <div class="d-flex flex-column my-2">
                            <button class="btn btn-dark" @click="sendTotalToParent(fabric)">Accept Order</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['manager'],
    computed: {
        Total() {
            // Calculate the total length of all colors in all fabrics
            let total = 0;
            for (const fabric of this.manager.fabrics) {
                for (const color of fabric.colors) {
                    total += color.length;
                }
            }
            return total;
        },
    },
    methods: {
        calculateTotal(colors) {
            // Calculate the total length of colors for a specific fabric
            let total = 0;
            for (const color of colors) {
                total += color.length;
            }
            return total;
        },
        sendTotalToParent(fabric) {
            console.log("Fabric Accepted pro:", fabric); // Check the output in the browser console
            this.$emit("parent-data", { total: this.calculateTotal(fabric.colors), fabric: fabric });
        },

        // sendFabric(fabric) {
        //     console.log("Fabric Accepted pro:", fabric); // Check the output in the browser console
        //     this.$emit("fabric", this.acceptedFabric = fabric);
        //     // this.$emit("total-calculated", this.calculateTotal(fabric.colors));
        // },

    }
}
</script>

<style lang="scss" scoped></style>