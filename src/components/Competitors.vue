<template>
    <div class="Competitors">
        <h1>DRAGONERA</h1>
        <h2>WHO ARE YOUR COMPETITORS?</h2>
        <span>Even if no one is offering the exact same product, please mention similar products or those targeting the same audience</span>
        <br><br>
        <div>
            <span>
                <textarea v-model="$store.state.productCompetitors.competitors"></textarea>
            </span>
            <br><br>
            <router-link to="/Solution">
                <span v-on:click="back">BACK</span>
            </router-link>
            <button @click="next">NEXT</button>
        </div>
        <div>
            <h2>PRODUCT SUMMARY</h2>
            <span v-for="detail in $store.state.productSummary" :key="detail.key">
                <span>
                    {{detail.text+':'+'  '+detail.value}}
                    <router-link v-bind:to="detail.id">
                        <span @click="edit(detail.text)">edit</span>
                    </router-link>
                </span>
                <br>
            </span>
            <button v-on:click="startOver">START OVER</button>
        </div>
    </div>
</template>

<script>   
    export default {
        name: 'competitors',
        data() {
            return {
            }
        },
        beforeMount: function () {
            for (var index = 0; index < this.$store.state.productSummary.length; index++) {
                    if ( this.$store.state.productSummary[index].text == 'Competitors') {
                        this.$store.state.productSummary[index].value = '';
                    }
                }
        },
        methods: {
            common: function () {
                for (var index = 0; index < this.$store.state.productSummary.length; index++) {
                    if ( this.$store.state.productSummary[index].text == 'Competitors') {
                        this.$store.state.productSummary[index].value = this.$store.state.productCompetitors.competitors;
                    }
                };
            },
            next: function () {
                this.common();
                this.$router.push('/Other');
            },
            back: function () {
                this.common();  
            },
            edit: function (name) {
                if (name === 'Competitors') {}
                else {
                    this.common();
                }
            },
            startOver: function () {
                 if (confirm('Are you sure you want to start a new Product?')) {
                    this.$store.state.productType.selected = '';
                    this.$store.state.productPurpose.checked = [];
                    this.$store.state.productPlatform.checked = [];
                    this.$store.state.productCategory.checked = [];
                    this.$store.state.productAudience.checked = [];
                    this.$store.state.productLogin.checked = [];
                    this.$store.state.productRevenue.checked = [];
                    this.$store.state.productAdmin.checked = [];
                    this.$store.state.productSolution.solution = '';
                    this.$store.state.productCompetitors.competitors = '';
                    this.$store.state.productOther.other = '';
                    this.$store.state.productName.name = '';

                    for (var index = 0; index < this.$store.state.productSummary.length; index++) {
                          this.$store.state.productSummary[index].value = '';
                    }
                    
                    this.$router.push('/');
                }
            }
        }
    }
</script>