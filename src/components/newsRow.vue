<template>
  <section class="news-row">
    <div class="row">
      <swiper ref="mySwiper2" :options="swiperOptions" v-if="news">
        <swiper-slide v-for="item in news" v-bind:key="item.id">
          <div class="news-card">
            <div class="news-img"
                 :style="{backgroundImage: 'url(\'' + (item.image.url ? item.image.url : 'slider1.png') +'\')'}">
              <div class="read-news">
                <router-link tag="a" :to="'/news/' + item.id" class="read-btn">
                  <img src="../assets/img/see.svg" alt="">
                </router-link>
              </div>
            </div>
            <div class="news-body">
              <div class="date">{{ new Date(item.publish_date * 1000).toLocaleDateString() }}</div>
              <h3>{{ item.name }}</h3>
              <p class="news-descr" v-html="item.preview.substring(0,100) + '...' "></p>
            </div>
          </div>
        </swiper-slide>
      </swiper>
    </div>


  </section>
</template>


<script>
import {mapGetters} from 'vuex'

export default {
  data() {
    return {
      swiperOptions: {
        slidesPerView: 4,
        spaceBetween: 20,
        loop: true,
        infinite: true,
        touchRatio: 1,
        centeredSlides: false,
        draggable: true,
        autoplay: {
          delay: 2500,
          disableOnInteraction: false,
        },
        breakpoints: {
          320: {
            slidesPerView: 1.5,
            centeredSlides: true,
            spaceBetween: 15,
            touchRatio: 1
          },
          768: {
            slidesPerView: 2,
            touchRatio: 1
          },
          1150: {
            slidesPerView: 4,
            spaceBetween: 20,
            touchRatio: 1
          }
        }

      }
    }
  },
  computed: {
    ...mapGetters({news: "news/getAll"}),
  },
  created() {
    this.$store.dispatch('news/loadAll')
  }
}
</script>
