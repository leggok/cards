<template>
    <div class="finnish">
        <div class="home-button">
            <btn-home/>
        </div>
        <div class="finnish_left">
            <div class="container">
                <div class="top">
                    <ul>
                        <li>
                            <div class="percent">{{ this.sadFinnishE }}%</div>
                            <div class="namen">First</div>
                        </li>
                        <li>
                            <div class="percent">{{ this.happyFinnishE }}%</div>
                            <div class="namen">Second</div>
                        </li>
                        <li>
                            <div class="percent">{{ this.heartFinnishE }}%</div>
                            <div class="namen">Third</div>
                        </li>
                    </ul>
                </div>
                <div class="finish_left_bottom">
                    <div class="res">Your res:</div>
                    <div class="title">COOL!!!</div>
                    <div class="sub_title">Lorem, ipsum dolor sit amet consectetur adipisicing elit. Modi ea dignissimos tempora qui dicta soluta laudantium odit omnis, officiis hic expedita culpa saepe, ad illum sed vel explicabo voluptas voluptate?</div>
                </div>
                <router-link to="/test" class="btn">Try again</router-link>
            </div>
        </div>        
    </div>
</template>

<style>
    @import url('../assets/css/fontello-embedded.css');
    .finnish{
        display: flex;
    }
</style>
<script>
import btnHome from '@/components/btn-home.vue';
export default {  
    components: {
        btnHome                 
    },
    data(){
        return{
            clc : 0,
            x: 0,
            happyFinnishE: 0,
            heartFinnishE: 0,
            sadFinnishE: 0
        }
    },
    props: ['happyFinnish', 'sadFinnish', 'heartFinnish'],
    mounted: function () {
        this.$nextTick(function () {            
            this.happyFinnishE = this.happyFinnish,
            this.heartFinnishE = this.heartFinnish,
            this.sadFinnishE = this.sadFinnish, 
            this.clc = 100 / (this.happyFinnishE + this.sadFinnishE + this.heartFinnishE);                  
            this.happyFinnishE = Math.round((this.clc) * this.happyFinnishE * 100) / 100
            this.heartFinnishE = Math.round(this.clc * this.heartFinnishE * 100) / 100
            this.sadFinnishE = Math.round(this.clc * this.sadFinnishE * 100) / 100
        })
    }
}
</script>