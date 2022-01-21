<template>
    <div class="grid md:grid-cols-2 gap-4">
        <!-- BOX 1 -->
        <div class="shadow-md bg-blue-100 p-10 text-center mb-4 rounded">
            <h3 class="text-3xl text-blue-900 font-bold mb-4">Cases</h3>
            <div class="text-2l mb-4">
                <span class="font-bold">New:</span>
                {{status.NewConfirmed}}
            </div>
            <div class="text-2l mb-4">
                <span class="font-bold">Total:</span>
                {{status.TotalConfirmed}}
            </div>
        </div>

        <!-- BOX 2 -->
        <div class="shadow-md bg-blue-300 p-10 text-center mb-4 rounded">
            <h3 class="text-3xl text-blue-900 font-bold mb-4">Deaths</h3>
            <div class="text-2l mb-4">
                <span class="font-bold">New:</span>
                {{status.NewDeaths }}
            </div>
            <div class="text-2l mb-4">
                <span class="font-bold">Total:</span>
                {{status.TotalDeaths }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'DataBoxes',
    props: ['status']
}
</script>