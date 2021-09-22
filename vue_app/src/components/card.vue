<template>
    <div class="card cardIn">
        <ul>
            <li>    
                <div class="card_top">                                                
                    <img class='card_top_img' v-bind:src="data[counter].img" alt="client">                                    
                </div>
                <div class="card_bottom">
                    <div class="name">{{ item.m_name }}</div>
                    <div class="description">{{ item.decr }}</div>
                </div>
                <div class="stamp">
                    First
                </div>                
            </li>                  
        </ul>
    </div>
</template>

<script>
export default {
  name: 'card',  
 
}
</script>
