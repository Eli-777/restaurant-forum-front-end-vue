<template>
  <div class="container py-5">
    <div>
      <h1>{{ restaurant.name }}</h1>
      <span class="badge badge-secondary mt-1 mb-3">
        {{ restaurant.Category.name ? restaurant.Category.name : '未分類'}}
      </span>
    </div>

    <hr>

    <ul>
      <li>評論數： {{ restaurant.Comments.length }}</li>
      <li>瀏覽次數： {{ restaurant.viewCounts }}</li>
    </ul>

    <button
      type="button"
      class="btn btn-link"
      @click="$router.back()"
    >
      回上一頁
    </button>
  </div>
</template>

<script>
const dummyData = {
  restaurant: {
    id: 30,
    name: "Nikita Boyer",
    tel: "(284) 625-0408 x71025",
    address: "101 Heidenreich Roads",
    opening_hours: "08:00",
    description:
      "Labore nihil ipsum quibusdam et laboriosam. Libero deleniti doloribus placeat sit velit rerum ipsam ut repudiandae. Aspernatur dolore doloremque eos. Molestiae animi ipsa labore officia.\n \rNon quaerat eos quidem aut quam facilis quia. Veniam soluta et excepturi ratione non eos repudiandae. Eos reprehenderit rerum soluta qui commodi dolorem rerum. Qui impedit unde alias deleniti. Doloremque unde distinctio.\n \rNumquam reiciendis ex pariatur tempore repellat. Perferendis nulla voluptatum et alias. Reiciendis inventore nihil atque et quia. Earum nobis aliquid voluptas error necessitatibus. Qui perspiciatis commodi aut qui est doloribus iure fuga.",
    image:
      "https://loremflickr.com/320/240/restaurant,food/?random=90.49719023698857",
    viewCounts: 1,
    createdAt: "2020-02-28T14:38:32.000Z",
    updatedAt: "2020-07-09T11:05:00.000Z",
    CategoryId: 2,
    Category: {
      id: 2,
      name: "日本料理",
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-02-28T14:38:32.000Z"
    },
    Comments: [
      {
        id: 30,
        text: "Facilis aut minus.",
        UserId: 3,
        RestaurantId: 30,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        User: {
          id: 3,
          name: "user2",
          email: "user2@example.com",
          password:
            "$2a$10$VHKmtPqbcUzK46qxLllqj.w506U2N2TObMmnpdlNG2CLZPa1xzuTi",
          isAdmin: true,
          image: "https://i.imgur.com/IaCnj2S.jpg",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-06-19T01:54:21.000Z"
        }
      },
      {
        id: 80,
        text: "Sunt quod nihil.",
        UserId: 2,
        RestaurantId: 30,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        User: {
          id: 2,
          name: "user1",
          email: "user1@example.com",
          password:
            "$2a$10$NyaAtgRuHx3i7hHlnb5IXOC4Uk4.q1J1iQs3op.ymdCEh7.tOwcH2",
          isAdmin: true,
          image: null,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-06-19T01:54:12.000Z"
        }
      },
      {
        id: 130,
        text: "Sit sit odio dolorum.",
        UserId: 1,
        RestaurantId: 30,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
          isAdmin: true,
          image: "https://i.imgur.com/kTEFFYJ.png",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-24T14:57:48.000Z"
        }
      }
    ]
  }
};

export default {
  data () {
    return {
      restaurant: dummyData.restaurant
    }
  },
  filters: {

  }
};
</script>