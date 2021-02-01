<template>

    <b-container>

       
       <b-button class="col-md-12" variant="primary" @click="hasHistory()? $router.go(-1): $router.push('/')">Volver</b-button>

       
        <Card :item="item" v-if="item" is-detail="0"></Card>


    </b-container>
</template>

<script>
    import Card from '../components/Card';

    export default {
        name:"Resumen",

        components: {
            Card
        },
        data() {
            return {
                item: {},
                trailer: {},
            }
        },
        methods:{
            hasHistory () { return window.history.length > 2 }
        },
        created() {
            this.$store.dispatch("fetchDetail", this.$route.params.id).then((item) => {
                if (item) {
                    this.$store.dispatch("fetchVideoTrailer", this.$route.params.id).then((par) => {
                        if (par) {

                            item["WTvideo"] = par.results;
                            this.item = item;
                        }
                    });
                }
            });
        }
    }
</script>

<style scoped>
    button{
     margin-top: 15px;
     margin-bottom: 15px;
    }
</style>