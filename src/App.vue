<template>
  <div>
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
        <text x="0" y="150" class = "text" mask="url(#halfMask)">{{ this.innerText }}</text>
        <text x="0" y="150" class = "text" fill ="black" mask="url(#Mask)">{{ this.innerText }}</text>
      </svg>
  </div>
</template>

<script>

export default {
  data(){
    return{
      blackWidth:0,
      innerText:'100',
      textWidth:0,
    }
  },

  methods:{
    getElementWidth(){
      let elem = this.$refs.svg;
      let bbox = elem.getBBox();
      this.textWidth = bbox.width;
    },

    animation(){
      const timer = setInterval(() => {
        this.blackWidth++;

        if(this.blackWidth > 300){
          clearInterval(timer);
        }
      }, 30)
    }
  },

  mounted(){
    this.getElementWidth();
    this.animation()
  },

  computed:{
    beigeWidth(){
      return Math.max(0, this.textWidth - this.blackWidth);
    }
  },

  watch:{
    
  }
}

</script>

<style>
  .text{
    font-size:200px;
    margin: 0;
    padding: 0;
  }

  svg{
    height: 200px;
  }
</style>