<template>
  <div class="home">
    <nova-receita></nova-receita>
  </div>
</template>

<script>
import NovaReceita from "@/components/receita";

export default {
  name: 'HomeView',
  components: {
    "nova-receita" : NovaReceita
  },
  data(){
    return{

    }
  },
  
}
</script>
