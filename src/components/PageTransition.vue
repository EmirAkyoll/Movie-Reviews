<template>
     <div>

      <button
        v-show="offsetNum !== 0"
        @click="prevPage"
        class="previous-button button flex-center">
        <img class="button-image" src="@/images/directionleft.png" alt="yonisaretisol"/>
         Previous Page
      </button>

      <button 
        @click="nextPage" 
        class="next-button button flex-center">
        Next Page
        <img class="button-image" src="@/images/directiontoright.png" alt="yonisaretisag"/>
      </button>

    </div>
</template>

<script>
export default {
    data(){ return{ offsetNum: 0, } },
    
    emits: ['page-transition'],
    
    methods: {

       nextPage() {
            this.offsetNum += 20;
            this.$emit('page-transition', this.offsetNum);
        },

        prevPage() {
            if(this.offsetNum !== 0){
                this.offsetNum -= 20;
                this.$emit('page-transition', this.offsetNum);
            }
        }
},
}
</script>

<style>
.previous-button{
  left: 140px;
}

.next-button{
  right: 140px;
}
</style>