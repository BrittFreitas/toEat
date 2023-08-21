<script setup lang="ts">
 import { ref} from 'vue'

// We must specify the data type that this array accepts, so we could just say <string[]> if it was an array of restaurant names for ex, but since we're going to be using an array of objects to add more details of eah restaurant we can utilize what's called an interface
const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({})

 // an interface is a way to define a type for an object
interface Restaurant {
  name?: string
  address?: string
  rating?: RecommendationStatus
  dishes?: Dish[]
}

// note that we get to reuse RecommendationStatus here, yay
interface Dish {
  name: string, 
  diet?: Diet, 
  recommendation: RecommendationStatus
}

type Diet = 'vegetarian' | 'vegan' | 'gluten-free' | 'pescatarian' | 'other'

type RecommendationStatus = 'Want to try'| 'Recommended' | 'Do Not Recommend' | 'Must Try'


function addRestaurant(){
  restaurantList.value.push({
    name: newRestaurant.value.name,
    address: newRestaurant.value.address,
    rating: newRestaurant.value.rating,
    dishes: []
  })
}

const ratingList = [
'Want to try', 'Recommended','Do Not Recommend','Must Try'
]


</script>

<template>
  <main class="main">
    <pre>
      {{ restaurantList }}
    </pre>
    
   <!-- create a form that allows users to add a restaurant to a list -->
   <form @submit.prevent="addRestaurant">
    <div>
      <label for="restaurantName">Restaurant Name</label>
      <input type="text" id="restaurantName" v-model="newRestaurant.name">
    </div>
    <div>
      <label for="restaurantAddress">Restaurant Address</label>
      <input type="text" id="restaurantAddress" v-model="newRestaurant.address">
    </div> 
    <div>
      <label for="restaurantSatus">Restaurant Rating</label>
    <select name="restarantStatus" id="restaurantStatus" v-model="newRestaurant.rating">
      <option v-for="rating in ratingList" :value="rating" :key="rating">{{ rating }}</option>
    </select>
    </div>
   
    

    <button type="submit">add restaurant</button>
  </form>

  <ul>
    <li v-for="restaurant in restaurantList" :key="restaurant.name">
      {{ restaurant.name }}  - {{ restaurant.rating }}
    </li>
  </ul>
  </main>
</template>

<style>
.main{
  width: 70%;
  border: red solid 2px;
margin: 0 auto
}
</style>