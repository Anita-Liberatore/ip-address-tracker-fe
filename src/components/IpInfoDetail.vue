<template>

    <div class=" card-detail
                absolute 
               -bottom-64 
               lg:-bottom-20 
               flex 
               flex-col 
               lg:flex-row 
               bg-white 
               gap-y-4 
               gap-x-12 
               px-40 
               pt-8 
               pb-12">

            <div class="flex flex-col row">
                <h3 class="font-bold mb-2 uppercase"> IP Address</h3>
                <span class="text-2xl">{{ipInfo.address}}</span>
            </div>

            <div class="flex flex-col row">
                <h3 class="font-bold mb-2 uppercase"> Location</h3>
                <span class="text-2xl">{{ipInfo.city}}</span>
            </div>

            <div class="flex flex-col row">
                <h3 class="font-bold mb-2 uppercase"> Timezone</h3>
                <span class="text-2xl">UTC {{ipInfo.timezone}}</span>
            </div>

            <div class="flex flex-col row">
                <h3 class="font-bold mb-2 uppercase"> Isp</h3>
                <span class="text-2xl">{{ipInfo.isp}}</span>
            </div>
        </div>
</template>

<script>
export default {
    props: ["ipInfo"],
};
</script>

<style scoped>
h3 {
    color: rgb(165, 159, 159);
    font-size: 18px;
}

span {
    font-weight: 700;
}

.card-detail {
    border-radius: 25px
}

/* Media Queries */
@media(max-width: 500px) {

    .card-detail {
        max-width: 80%;
        padding: 10px 0 10px 0;
    }

    .row {
        align-items: center;
    }

    span {
        text-align: center;
        font-size: 20px;
        width: 80%;
    }

    h3 {
        font-size: 15px;
    }
}

/* Media Queries */
@media(max-width: 1024px) {

.card-detail {
    padding: 10px 0 10px 0;
}

.row {
    align-items: center;
}

span {
    text-align: center;
    font-size: 20px;
    width: 80%;
}

h3 {
    font-size: 15px;
}
}
</style>