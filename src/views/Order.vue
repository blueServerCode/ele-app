<template>
    <div class="order">
        <div class="title">
            <span>订单</span>
            <i class="fa fa-search"></i>
        </div>
        <div class="remind">您还没有订单!</div>
        <div class="recommend">—————— 为您推荐附近精选 ——————</div>
        <div class="shoplist" v-for="(item, index) in restaurants" :key="index">
            <IndexShop class="shop" :restaurant="item.restaurant" />
        </div>
    </div>
</template>

<script>
import IndexShop from "../components/IndexShop";
export default {
    name: "order",
    components: {
        IndexShop,
    },
    data() {
        return {
            restaurants: [],
            page: 1,
            size: 5,
        };
    },
    mounted() {
        this.loadData();
    },
    methods: {
        loadData() {
            // 拉取商家信息
            this.$axios
                .post(
                    `/api/profile/restaurants/${this.page}/${this.size}`,
                    this.data
                )
                .then((res) => {
                    console.log(res.data);
                    this.restaurants = res.data;
                });
        },
    },
};
</script>

<style scoped>
.order {
    width: 100%;
    height: 100%;
    box-sizing: border-box;
    background-color: rgb(245, 245, 245);
}
.title {
    font-weight: 550;
    font-size: 18px;
    padding: 10px;
    background-color: rgb(0, 143, 255);
    color: white;
    padding-top: 15px;
    padding-bottom: 15px;
}
.title span {
    margin-right: 300px;
}
.remind {
    margin-top: 60px;
    margin-left: 140px;
    font-size: 18px;
    color: gray;
}
.recommend {
    font-size: 15px;
    color: gray;
    margin-top: 60px;
    text-align: center;
    padding: 10px;
}
.shoplist {
    padding: 5px;
    border-bottom: 0.5px solid gray;
}
.shop {
    border-radius: 10px;
}
</style>
