<template>  
    <div class="flexable">
        <div class="left">
            <div class="top">
                <btnHome />
                <a href="#" class="menu restart" @click="refreshElems"><i class="icon-arrows-cw"></i></a>
            </div>
            <div class="middle">
                <span class="param">Parameters:</span>
                <div class="indicators">
                    <div class="emotion">
                        <span class="circle"><i class="icon-frown"></i></span>
                        <span class="number">{{ sad }}</span>
                    </div>
                    <div class="emotion">
                        <span class="circle"><i class="icon-smile"></i></span>
                        <span class="number">{{ happy }}</span>
                    </div>
                    <div class="emotion">
                        <span class="circle"><i class="icon-heart"></i></span>
                        <span class="number">{{ heart }}</span>
                    </div>
                </div>
            </div>
            <div class="bottom">
                <span class="queue">Queue:</span>
                <span class="numb"><span class="count">{{index}}</span>/15 </span>
            </div>
        </div>
        <div class="right">
            <div class="wrap db" :id="'w'+item.id" v-for="item in data" :key="item.id">
                <div class="card cardIn" v-if="index === item.id">                
                    <div>                     
                        <div class="card_top">                                                
                            <img class='card_top_img' v-bind:src="item.img" alt="client">                                    
                        </div>
                        <div class="card_bottom">
                            <div class="name">{{ item.m_name}}</div>
                            <div class="description">{{ item.decr }}</div>
                        </div>
                        <div class="stamp" v-bind:class="{ stampAnimFirst: isStampFirstA, stampAnimSecond: isStampSecondA, stampAnimThird: isStampThirdA }">
                            First
                        </div>                                            
                    </div>
                </div>
            </div>
            <div class="buttons">                
                <a href="#" id="first" class="btn" v-on:click='sadF(); final(); isStampFirst();'>First</a>
                <a href="#" id="second" class="btn" v-on:click='happyF(); final(); isStampSecond();'>Second</a>
                <a href="#" id="third" class="btn" v-on:click='heartF(); final(); isStampThird();'>Third</a>                
            </div>                        
        </div>                 
    </div> 
</template>

<style>
    @import url('../assets/css/fontello-embedded.css');
    .left{     
        height: 100vh;
    }    
    .flexable{
        display: flex;
    }
    .right{
        justify-content: unset;
    }
</style>

<script>
import JQuery from 'jquery'
let $ = JQuery
import btnHome from '@/components/btn-home.vue';
export default {  
    components: {
        // card,
        btnHome
    },    
    data(){
        return {
            data:[],      
            asd : '',
            item:1,
            index: 1,
            sad:0,
            happy:0,
            heart:0,
            isStampFirstA: false,
            isStampSecondA: false,
            isStampThirdA: false
        }
    },
    mounted(){
        
        fetch('./clients.json')
            .then((response) => {                
                return response.json();
            })
            .then((data) => {
                console.log(data);
                this.data = data
                this.asd = data[this.item].m_name
            })   
        $('#w'+this.index).addClass('db')               
    },    
    methods: {        
        isStampFirst: function(){
            this.isStampFirstA = true;
            var self = this;            
            setTimeout(function(){
                $('.card').addClass('cardOutFirst')
                setTimeout(function(){
                    self.isStampFirstA = false;
                    self.index++;                                
                },1000)
            },1000)
        },
        isStampSecond: function(){
            this.isStampSecondA = true;
            var self = this;
            $('.stamp').text('Second');
            setTimeout(function(){
                $('.card').addClass('cardOutSecond')
                setTimeout(function(){
                    self.isStampSecondA = false;
                    self.index++;                                
                },1000)
            },1000)
        },
        isStampThird: function(){
            this.isStampThirdA = true;
            var self = this;
            $('.stamp').text('Third');
            setTimeout(function(){
                $('.card').addClass('cardOutThird')
                setTimeout(function(){
                    self.isStampThirdA = false;
                    self.index++;            
                },1100)
            },1000)
        },
        sadF: function(){
            this.sad++;            
        },  
        happyF: function(){
            this.happy++
        },       
        heartF: function(){
            this.heart++
        },            
        final: function(){
            if (this.index >= '15'){
                let happyFinnish = this.happy;
                let sadFinnish = this.sad;
                let heartFinnish = this.heart;
                var self = this;
                setTimeout(function(){
                    self.$router.push({ name: 'Finnish', params: { happyFinnish, sadFinnish, heartFinnish }})             
                }, 2500)
            }
        },
        refreshElems: function(){                        
            this.item = 1,
            this.index = 1,
            this.sad = 0,
            this.happy = 0,
            this.heart = 0 
        }        
    }
}
</script>