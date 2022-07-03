<template>
  <div>
      <div class="p-8 text-center bg-[#2a2a8f] text-white mb-4 relative">
          <div class="bg-white p-2 absolute img-div">
            <img src="https://www.kloudcommerce.co/images/brand/colored-brand-logo.png">
          </div>
        <h1 class="sm:text-4xl text-2xl mb-4">KLOUD COMMERCE CHALLENGE</h1>

        <div id="carouselExampleIndicators" class="carousel slide" data-ride="carousel">
            <div class="carousel-inner">
                <div class="carousel-item active">
                    <p class="font-thin">Have fun</p>
                </div>
                <div class="carousel-item">
                    <p class="font-thin">Create</p>
                </div>
                <div class="carousel-item">
                    <p class="font-thin">Explore</p>
                </div>
            </div>

            <ol class="carousel-indicators relative carousel-ol">
                <li data-target="#carouselExampleIndicators" data-slide-to="0" class="active"></li>
                <li data-target="#carouselExampleIndicators" data-slide-to="1"></li>
                <li data-target="#carouselExampleIndicators" data-slide-to="2"></li>
            </ol>
        </div>
      </div>
  </div>
</template>

<script>
export default {
    created(){
        this.slideCarousel()
    },
    methods:{
        slideCarousel(){
            $('.carousel').carousel({
                interval: 1000
            })
        }
    }

}
</script>

<style scoped>
.img-div{
    width:190px; 
    top:-25px
}
.carousel-ol{
    top:30px;
}

</style>