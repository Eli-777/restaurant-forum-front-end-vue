<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">美食達人</h1>
    <hr />
    <div class="row text-center">
      <div 
        v-for="user in users" 
        :key="user.id"  
        class="col-3"
      >
        <router-link 
          :to="{ name: 'user', params: { id: user.id }}"
        >
          <img :src="user.image | noImage" width="140px" height="140px" />
        </router-link>
        <h2>{{user.name}}</h2>
        <span class="badge badge-secondary">追蹤人數：{{user.FollowerCount}}</span>
        <p class="mt-3">
          <button type="button" v-if="user.isFollowed" class="btn btn-danger" @click.stop.prevent="deleteFollow(user.id)">取消追蹤</button>
          <button type="button" v-else class="btn btn-primary" @click.stop.prevent="addFollow(user.id)">追蹤</button>
        </p>
      </div>
    </div>
  </div>
</template>


<script>
import NavTabs from "./../components/Navtabs";
import usersAPI from './../apis/users.js'
import { Toast } from './../utils/helpers'



export default {
  components: {
    NavTabs
  },
  data () {
    return {
      users: []
    }
  },
  created () {
    this.fetchUsers ()
  },
  methods: {
    async fetchUsers () {
      try {
        const { data } = await usersAPI.getTopUsers()
        this.users = data.users
      } catch (error) {
        console.log('error', error)
        Toast.fire({
          icon: 'error',
          title: '無法取得美食達人，請稍後再試'
        })
      }
      
    },
    async addFollow (userId) {
      try {
        const { data } = await usersAPI.addFollowing({ userId })
        if ( data.status !== 'success') {
          throw new Error(data.message)
        }

        this.users.forEach( user => {
          if(user.id === userId) {
            user.isFollowed = true;
          } else {
            return user
          }
        })
      } catch (error) {
        console.log('error', error)
        Toast.fire({
          icon: 'error',
          title: '無法加入追蹤，請稍後再試'
        })
      }
      
    },
    async deleteFollow (userId) {
      try {
        const { data } = await usersAPI.deleteFollowing({ userId })
        if (data.status !== 'success') {
          throw Error(data.message)
        }
        this.users.map( user => {
          if(user.id === userId) {
            user.isFollowed = false;
          } else {
            return user
          }
        })

      } catch(error) {
        console.log('error', error)
        Toast.fire({
          icon: 'error',
          title: '無法取消追蹤，請稍後再試'
        })
      }
      
    }
  },
  filters: {
    noImage (userImage) {
      if (!userImage) return "http://via.placeholder.com/300x300?text=No+Image"
      return userImage
    }
  }
};
</script>