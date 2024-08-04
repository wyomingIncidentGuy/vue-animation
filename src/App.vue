<template>
  <div>
    <input type="text" v-model="this.innerText">
    <svg 
        ref="svg"
        xmlns="http://www.w3.org/2000/svg"
        fill="beige">
        <mask id="halfMask">
            <rect x="0" y="0" :width="this.beigeWidth" height="200" fill="white" />
        </mask>
        <mask id="Mask">
            <rect :x="this.beigeWidth" y="0" :width="this.blackWidth" height="200" fill="white" />
        </mask>
        <text x="" y="150" stroke-width="5" class = "text" mask="url(#halfMask)">{{ innerText }}</text>
        <text x="" y="150" stroke-width="5" class = "text" fill ="black" mask="url(#Mask)">{{ innerText }}</text>
      </svg>
      <p>{{ this.textWidth }}</p>
  </div>
</template>

<script>

export default {
  data(){
    return{
      blackWidth:50,
      innerText:'text',
      textWidth:0
    }
  },

  methods:{
    getElementWidth(){
      let elem = this.$refs.svg;
      let bbox = elem.getBBox();
      this.textWidth = bbox.width;
    }
  },

  mounted(){
    this.getElementWidth()
  },

  computed:{
    beigeWidth(){
      return this.textWidth - this.blackWidth;
    }
  },

  watch:{
    
  }
}

</script>

<style>
  .text{
    font-size:200px;
  }

  svg{
    height: 250px;
  }
</style>