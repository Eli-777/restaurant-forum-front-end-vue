<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">人氣餐廳</h1>

    <hr />
    <!-- 人氣餐廳卡片 RestaurantCard-->
    <RestaurantTopCard 
      v-for="restaurant in restaurants" 
      :key="restaurant.id"
      :initial-restaurant="restaurant"  
    />
  </div>
</template>

<script>
import NavTabs from "./../components/Navtabs";
import RestaurantTopCard from './../components/RestaurantTopCard'
import restaurantsAPI from './../apis/restaurants'
import { Toast } from './../utils/helpers'



export default {
  components: {
    NavTabs,
    RestaurantTopCard
  },
  data () {
    return {
     restaurants: []
    }
  },
  created () {
    this.fetchRestaurants ()
  },
  methods: {
    async fetchRestaurants () {
      try {
        const { data } = await restaurantsAPI.getTopRestaurants()
        this.restaurants = data.restaurants
      } catch (error) {
        console.log('error', error)
        Toast.fire({
          icon: 'error',
          title: '無法取得人氣餐廳，請稍後再試'
        })
      }
    },
  }
};
</script>