<template>
	<div>
  	<div class="row">
      <div class="col-xs-12 col-xl-8 offset-xl-2 col-lg-8 offset-lg-2">
        <div class="q-pa-md">
          <q-carousel 
            arrows
            animated
            v-model="slide"
            height="600px"
            class="gt-sm"
            infinite
            swipeable
          >
            <q-carousel-slide v-for="(app, $index) in aplications" :key="$index" v-if="$index < 3"
            v-bind:name="$index +1" v-bind:img-src="app.image_url">
              <div class="absolute-bottom custom-caption" style="background-color: rgba(0, 0, 0, 0.79);">
                <div class="text-h6">{{ app.name }}</div>
              </div>
              <div v-if="app.published == false">
                <q-badge color="red">
                  No verificada <q-icon name="warning" color="white" class="q-ml-xs" />
                </q-badge>
              </div>
              <div v-else-if="app.published == true">
                <q-badge color="green">
                  Verificada <q-icon name="check" color="white" class="q-ml-xs" />
                </q-badge>
              </div>
            </q-carousel-slide>
          </q-carousel>
          <q-carousel  
            arrows
            animated
            v-model="slide"
            height="200px"
            class="lt-md"
            infinite
            swipeable
          >
            <q-carousel-slide v-for="(app, $index) in aplications" :key="$index" v-if="$index < 3"
            v-bind:name="$index +1" v-bind:img-src="app.image_url">
              <div class="absolute-bottom custom-caption" style="background-color: rgba(0, 0, 0, 0.79);">
                <div class="text-h6">{{ app.name }}</div>
              </div>
            </q-carousel-slide>
          </q-carousel>
        </div>
      </div>
    </div>
    <div class="row q-col-gutter-lg">
      <div class="col-xs-12 col-sm-6 col-md-4 col-lg-3" v-for="(app, $index) in aplications" :key="$index">
        <a v-bind:href="'#/aplication/'+ app.id">
        <q-img
          :ratio="16/9"
          v-bind:src="app.image_url"
          style="width: 100%"
          class="zoom"
        >
          <div class="absolute-bottom text-subtitle1 text-center text-white q-pa-xs">
            <a v-bind:href="'#/aplication/'+ app.id" style="color: #00d999; text-decoration: none;"> {{app.name}} </a>
          </div>
          <div v-if="app.published == false">
            <q-badge color="red">
              No verificada <q-icon name="warning" color="white" class="q-ml-xs" />
            </q-badge>
          </div>
          <div v-else-if="app.published == true">
            <q-badge color="green">
              Verificada <q-icon name="check" color="white" class="q-ml-xs" />
            </q-badge>
          </div>
        </q-img>
        </a>   
      </div>
    </div>
    
    <!--<div class="row"> 
     	<div class="col-xs-12 col-sm-4 col-md-3 col-lg-2 col-xl-2"  v-for="n in 6" :key="`none-${n}`">
    		<div class="q-pa-md">
          <div class="q-col-gutter-xs row items-start">
            <q-img
              src="https://cdn.quasar.dev/img/parallax2.jpg"
              style="width: 100%"
            >
              <div class="absolute-bottom text-subtitle1 text-center q-pa-xs">
                Caption
              </div>
            </q-img>
          </div>
        </div>
      </div>
    </div>!-->
  </div>
</template>

<style>
</style>

<script>

import Carousel from 'layouts/Carousel.vue'
import Card from 'layouts/Card.vue'


export default {
  name: 'PageIndex',
  components: {
    Carousel,
    Card,
  },
  data () {
    return {
      aplications: null,
      model: null,
      slide: 1
    }
  },
  created () {
    this.$axios.get("/api/v1/apps")
        .then(request => { this.aplications = request.data.data
          })
   },
}
</script>


<style>
	.center {
	  margin: auto;
	  width: 80%;
	}
  .custom-caption{
    text-align: center;
    padding: 12px;
    color: white;
    background-color: rgba(0, 0, 0, .3);
  }
  .a{
    color: white;
  }
  .zoom {
  transition: transform .2s;
  }
  .zoom:hover {
    -ms-transform: scale(1.08); /* IE 9 */
    -webkit-transform: scale(1.08); /* Safari 3-8 */
    transform: scale(1.08); 
  }
</style>

