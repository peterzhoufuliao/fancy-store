<template>
    <div class="page orderpage">
        <v-touch @swipeleft="onSwipeLeft()" @swiperight="onSwipeRight()">
            <headersec tabname="我的订单" ref="noback"></headersec> <ordertab :urlRouter="$route.path"></ordertab>
            <transition :name="slidename">
                <div class="ordercontainer" v-show="mainarea">
                    <img src="../../../public/img/github.png" alt />
                    <p>待发货页面</p>
                </div>
            </transition>
        </v-touch>
    </div>
</template>

<script>
import { mapGetters, mapMutations } from "vuex";
export default {
    data() {
        return {};
    },
    components: {
        Headersec: () => import("../../components/HeaderSec"),
        Ordertab: () => import("../../components/OrderTab")
    },
    computed: {
        ...mapGetters(["this.$store.state.ordercur"])
    },
    mounted() {
        this.$refs.noback.isBack = false;
        this.setOrdercur(3);
        this.$store.state.ordercur < this.$store.state.ordertab ? (this.slidename = "slide-back") : (this.slidename = "slide-go");
        this.setOrdertab(3);
    },
    methods: {
        onSwipeLeft() {
            this.$router.push("./waitreceive");
        },
        onSwipeRight() {
            this.$router.push("./waitpay");
        },
        ...mapMutations({
            setOrdercur: "SET_ORDERCUR",
            setOrdertab: "SET_ORDERTAB"
        })
    }
};
</script>
