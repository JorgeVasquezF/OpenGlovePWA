<template>
  <!-- SI ESTA VERIFICADA !-->
	<div v-if="aplication.published == true">
    <div class="q-pa-lg">
      <div class="row">
        <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 col-xl-4 offset-xl-2 offset-lg-2">
          <q-img
              v-bind:src="aplication.image_url"
              style="width: 100%"
            >
              <div class="absolute-bottom text-subtitle1 text-center q-pa-xs">
               {{aplication.name}}
              </div>
            </q-img>
        </div>
        <div class="q-pa-lg">
          <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 col-xl-4 q-gutter-x-xs">
            <h6 class="q-pa-xs q-mt-xs q-mb-md">{{aplication.name}}</h6> 
            <h6 class="q-pa-xs q-mt-xs q-mb-md">Autor: shoxo</h6>
            <h6 class="q-pa-xs q-mt-xs q-mb-md">{{aplication.os}}</h6>
            <q-rating class="q-mb-md"
              v-model="averageRating"
              size="2em"
              color="orange"
              readonly
            />
            <q-space/>
            
            <q-btn type="a" v-bind:href="lastRelease" label="Descargar" color="primary" />
            <q-badge align="middle">{{releases[0].tag_name}}</q-badge>
          </div>
        </div>
      </div>
  </div>
    <div class="row">
      <div class="q-pa-xs col-xs-12 text-white col-lg-8 col-xl-8 offset-lg-2 offset-xl-2">
        <q-list dark padding bordered class="rounded-borders " style="max-width: 1500px">
          <q-expansion-item
            icon="format_italic"
            label="Descripción"
            class="itemLabel"
          >
            <q-card class="bg-twitch">
              <q-card-section>
                <h6 style="color: #ffffff">
                  {{aplication.description}}
                </h6>
                <div class="embed-container">
                    <iframe width="560" height="315" v-bind:src="aplication.video_url"allowfullscreen></iframe>
                </div>
              </q-card-section>
            </q-card>
          </q-expansion-item>
          <q-expansion-item
            icon="description"
            label="Documentación"
            class="itemLabel"
          >
            <q-card class="bg-twitch">
              <q-card-section>
                <h6 style="color: #ffffff">{{aplication.documentation}}</h6>
              </q-card-section>
            </q-card>
          </q-expansion-item>
          <q-expansion-item
            icon="cloud_download"
            label="Releases"
            header-class="text-orange"
            class="itemLabel"
          >
            <q-card class="bg-twitch">
              <q-card-section>
                <div class="q-pa-md" style="max-width: 350px">
                  <!--<li v-for="release in releases">
                         <a v-bind:href="release.zipball_url"> {{release.tag_name}} </a>
                      </li> -->
                  <q-list dense bordered padding class="rounded-borders">
                    <q-item clickable v-ripple v-for="(release, $index) in releases" :key="$index">
                      
                      <q-item-section>
                        <a v-bind:href="release.zipball_url" style="color: #ff9800 "> {{release.tag_name}} </a>
                      </q-item-section>
                    </q-item>

                    
                  </q-list>
                </div>
              </q-card-section>
            </q-card>
          </q-expansion-item>
        </q-list>
      </div>
    </div>
    <div class="row">
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-4 offset-xl-4 text-center text-orange">
        <h6 class="q-mb-xs">Escribe tu review</h6>
      </div>
    </div>
    <div class="row">
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-3 offset-xl-3">
        <q-input dark outlined bottom-slots v-model="email" type="email" label="Nombre" >
          <template v-slot:prepend>
            <q-icon name="perm_identity" />
          </template>
          <template v-slot:append>
            <q-icon name="close" @click="email = ''" class="cursor-pointer" />
          </template>
        </q-input>
      </div>
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-3">
        <q-input dark outlined bottom-slots v-model="email" type="email" label="Email" >
            <template v-slot:prepend>
              <q-icon name="mail" />
            </template>
            <template v-slot:append>
              <q-icon name="close" @click="email = ''" class="cursor-pointer" />
            </template>
          </q-input>
      </div>
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-6 offset-xl-3">
        <q-input
          dark 
          outlined
          v-model="text"
          type="textarea"
        />
      </div>
    </div>
    <div v-for="rating in ratings" class="row">
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-6 offset-xl-3">
        <q-rating class="q-mb-xs q-mt-lg" 
        v-model="rating.rating"
        size="1em"
        readonly
        />
        <h6 class="q-pa-xs q-mt-xs q-mb-xs q-mr-xs" >{{rating.user.username}}</h6>
        <h6 class="q-pa-xs q-mt-xs q-mb-xs float-left" >"{{rating.comment}}"</h6> 
      </div>
    </div>  
  	<!--<div class="row">
      <div class="col-xs-12 col-xl-8 offset-xl-2 col-lg-8 offset-lg-2">
        <Carousel />
      </div>
    </div>!-->
  </div>
  <!-- SI NO ESTA VERDIFICADA Y ES EL DUEñO !-->
  <div v-else-if="aplication.published == false && usercheck[0].role == 1">
    <div class="q-pa-lg">
      <div class="row">
        <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 col-xl-6 offset-xl-3 offset-lg-2">
          <h6>Tu aplicación esta siendo revisada</h6>
        </div>
        <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 col-xl-4 offset-xl-2 offset-lg-2">
          <q-img
              v-bind:src="aplication.image_url"
              style="width: 100%"
            >
              <div class="absolute-bottom text-subtitle1 text-center q-pa-xs">
               {{aplication.name}}
              </div>
            </q-img>
        </div>
        <div class="q-pa-lg">
          <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 col-xl-4 q-gutter-x-xs">
            <h6 class="q-pa-xs q-mt-xs q-mb-md">{{aplication.name}}</h6> 
            <h6 class="q-pa-xs q-mt-xs q-mb-md">Autor: shoxo</h6>
            <h6 class="q-pa-xs q-mt-xs q-mb-md">{{aplication.os}}</h6>
            <q-rating class="q-mb-md"
              v-model="averageRating"
              size="2em"
              color="orange"
              readonly
            />
            <q-space/>
            <q-btn type="a" v-bind:href="lastRelease" label="Descargar" color="primary" />
            <q-badge align="middle">{{releases[0].tag_name}}</q-badge>
          </div>
        </div>
      </div>
  </div>
    <div class="row">
      <div class="q-pa-xs col-xs-12 text-white col-lg-8 col-xl-8 offset-lg-2 offset-xl-2">
        <q-list dark padding bordered class="rounded-borders " style="max-width: 1500px">
          <q-expansion-item
            icon="format_italic"
            label="Descripción"
            class="itemLabel"
          >
            <q-card class="bg-twitch">
              <q-card-section>
                <h6 style="color: #ffffff">
                  {{aplication.description}}
                </h6>
                <div class="embed-container">
                    <iframe width="560" height="315" v-bind:src="aplication.video_url"allowfullscreen></iframe>
                </div>
              </q-card-section>
            </q-card>
          </q-expansion-item>
          <q-expansion-item
            icon="description"
            label="Documentación"
            class="itemLabel"
          >
            <q-card class="bg-twitch">
              <q-card-section>
                <h6 style="color: #ffffff">{{aplication.documentation}}</h6>
              </q-card-section>
            </q-card>
          </q-expansion-item>
          <q-expansion-item
            icon="cloud_download"
            label="Releases"
            header-class="text-orange"
            class="itemLabel"
          >
            <q-card class="bg-twitch">
              <q-card-section>
                <h6 style="color: #ffffff"> Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quidem, eius reprehenderit eos corrupti
                commodi magni quaerat ex numquam, dolorum officiis modi facere maiores architecto suscipit iste
                eveniet doloribus ullam aliquid.</h6>
              </q-card-section>
            </q-card>
          </q-expansion-item>
        </q-list>
      </div>
    </div>
    <div class="row">
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-4 offset-xl-4 text-center text-orange">
        <h6 class="q-mb-xs">Escribe tu review</h6>
      </div>
    </div>
    <div class="row">
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-3 offset-xl-3">
        <q-input dark outlined bottom-slots v-model="email" type="email" label="Nombre" >
          <template v-slot:prepend>
            <q-icon name="perm_identity" />
          </template>
          <template v-slot:append>
            <q-icon name="close" @click="email = ''" class="cursor-pointer" />
          </template>
        </q-input>
      </div>
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-3">
        <q-input dark outlined bottom-slots v-model="email" type="email" label="Email" >
            <template v-slot:prepend>
              <q-icon name="mail" />
            </template>
            <template v-slot:append>
              <q-icon name="close" @click="email = ''" class="cursor-pointer" />
            </template>
          </q-input>
      </div>
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-6 offset-xl-3">
        <q-input
          dark 
          outlined
          v-model="text"
          type="textarea"
        />
      </div>
    </div>
    <div v-for="rating in ratings" class="row">
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-6 offset-xl-3">
        <q-rating class="q-mb-xs q-mt-lg" 
        v-model="rating.rating"
        size="1em"
        readonly
        />
        <h6 class="q-pa-xs q-mt-xs q-mb-xs q-mr-xs" >{{rating.user.email}}</h6>
        <h6 class="q-pa-xs q-mt-xs q-mb-xs float-left" >"{{rating.comment}}"</h6> 
      </div>
    </div> 
  </div>
  <div v-else-if="aplication.published == false && usercheck[0].role == 1">
    <div class="q-pa-lg">
      <div class="row">
        <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 col-xl-4 offset-xl-2 offset-lg-2">
          <h6>Tu aplicación esta siendo revisada</h6>
        </div>
        <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 col-xl-4 offset-xl-2 offset-lg-2">
          <q-img
              v-bind:src="aplication.image_url"
              style="width: 100%"
            >
              <div class="absolute-bottom text-subtitle1 text-center q-pa-xs">
               {{aplication.name}}
              </div>
            </q-img>
        </div>
        <div class="q-pa-lg">
          <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 col-xl-4 q-gutter-x-xs">
            <h6 class="q-pa-xs q-mt-xs q-mb-md">{{aplication.name}}</h6> 
            <h6 class="q-pa-xs q-mt-xs q-mb-md">Autor: shoxo</h6>
            <h6 class="q-pa-xs q-mt-xs q-mb-md">{{aplication.os}}</h6>
            <q-rating class="q-mb-md"
              v-model="averageRating"
              size="2em"
              color="orange"
              readonly
            />
            <q-space/>
            <q-btn color="primary" label="Descargar" />
            <q-badge align="middle">{{releases[0].tag_name}}</q-badge>
          </div>
        </div>
      </div>
  </div>
    <div class="row">
      <div class="q-pa-xs col-xs-12 text-white col-lg-8 col-xl-8 offset-lg-2 offset-xl-2">
        <q-list dark padding bordered class="rounded-borders " style="max-width: 1500px">
          <q-expansion-item
            icon="format_italic"
            label="Descripción"
            class="itemLabel"
          >
            <q-card class="bg-twitch">
              <q-card-section>
                <h6 style="color: #ffffff">
                  {{aplication.description}}
                </h6>
                <div class="embed-container">
                    <iframe width="560" height="315" v-bind:src="aplication.video_url"allowfullscreen></iframe>
                </div>
              </q-card-section>
            </q-card>
          </q-expansion-item>
          <q-expansion-item
            icon="description"
            label="Documentación"
            class="itemLabel"
          >
            <q-card class="bg-twitch">
              <q-card-section>
                <h6 style="color: #ffffff">{{aplication.documentation}}</h6>
              </q-card-section>
            </q-card>
          </q-expansion-item>
          <q-expansion-item
            icon="cloud_download"
            label="Releases"
            header-class="text-orange"
            class="itemLabel"
          >
            <q-card class="bg-twitch">
              <q-card-section>
                <h6 style="color: #ffffff"> {{lastRelease}}</h6>
              </q-card-section>
            </q-card>
          </q-expansion-item>
        </q-list>
      </div>
    </div>
    <div class="row">
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-4 offset-xl-4 text-center text-orange">
        <h6 class="q-mb-xs">Escribe tu review</h6>
      </div>
    </div>
    <div class="row">
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-3 offset-xl-3">
        <q-input dark outlined bottom-slots v-model="email" type="email" label="Nombre" >
          <template v-slot:prepend>
            <q-icon name="perm_identity" />
          </template>
          <template v-slot:append>
            <q-icon name="close" @click="email = ''" class="cursor-pointer" />
          </template>
        </q-input>
      </div>
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-3">
        <q-input dark outlined bottom-slots v-model="email" type="email" label="Email" >
            <template v-slot:prepend>
              <q-icon name="mail" />
            </template>
            <template v-slot:append>
              <q-icon name="close" @click="email = ''" class="cursor-pointer" />
            </template>
          </q-input>
      </div>
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-6 offset-xl-3">
        <q-input
          dark 
          outlined
          v-model="text"
          type="textarea"
        />
      </div>
    </div>
    <div v-for="rating in ratings" class="row">
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-6 offset-xl-3">
        <q-rating class="q-mb-xs q-mt-lg" 
        v-model="rating.rating"
        size="1em"
        readonly
        />
        <h6 class="q-pa-xs q-mt-xs q-mb-xs q-mr-xs" >{{rating.user.email}}</h6>
        <h6 class="q-pa-xs q-mt-xs q-mb-xs float-left" >"{{rating.comment}}"</h6> 
      </div>
    </div> 
  </div>
  <!-- ###############################################################################3
    ###################################################################################3
    ###################################################################################3!-->
    <!-- SI NO ESTA VERDIFICADA Y ES REVISADOR !-->
  <div v-else-if="aplication.published == false && usercheck[0].role == 2">
    <div class="q-pa-lg">
      <div class="row">
        <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 col-xl-6 offset-xl-3 offset-lg-2">
          
          <div class="q-gutter-sm q-pa-md">
            <h6>Revisa la aplicación</h6>
            <q-input
              v-model="comment"
              filled
              type="textarea"
              dark
            />
            <q-btn color="primary" label="Aprobar" @click="checkApp()"/>
            <q-btn color="red" label="Rechazar" />
            <h6 v-show="completed == true">Gracias!</h6>
          </div>
           
        </div>
      </div>
      <div class="row">
        <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 col-xl-4 offset-xl-2 offset-lg-2">
          <q-img
              v-bind:src="aplication.image_url"
              style="width: 100%"
            >
              <div class="absolute-bottom text-subtitle1 text-center q-pa-xs">
               {{aplication.name}}
              </div>
            </q-img>
        </div>
        <div class="q-pa-lg">
          <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 col-xl-4 q-gutter-x-xs">
            <h6 class="q-pa-xs q-mt-xs q-mb-md">{{aplication.name}}</h6> 
            <h6 class="q-pa-xs q-mt-xs q-mb-md">Autor: shoxo</h6>
            <h6 class="q-pa-xs q-mt-xs q-mb-md">{{aplication.os}}</h6>
            <q-rating class="q-mb-md"
              v-model="averageRating"
              size="2em"
              color="orange"
              readonly
            />
            <q-space/>
            <q-btn type="a" v-bind:href="lastRelease" label="Descargar" color="primary" />
            <q-badge align="middle">{{releases[0].tag_name}}</q-badge>
          </div>
        </div>
      </div>
  </div>
    <div class="row">
      <div class="q-pa-xs col-xs-12 text-white col-lg-8 col-xl-8 offset-lg-2 offset-xl-2">
        <q-list dark padding bordered class="rounded-borders " style="max-width: 1500px">
          <q-expansion-item
            icon="format_italic"
            label="Descripción"
            class="itemLabel"
          >
            <q-card class="bg-twitch">
              <q-card-section>
                <h6 style="color: #ffffff">
                  {{aplication.description}}
                </h6>
                <div class="embed-container">
                    <iframe width="560" height="315" v-bind:src="aplication.video_url"allowfullscreen></iframe>
                </div>
              </q-card-section>
            </q-card>
          </q-expansion-item>
          <q-expansion-item
            icon="description"
            label="Documentación"
            class="itemLabel"
          >
            <q-card class="bg-twitch">
              <q-card-section>
                <h6 style="color: #ffffff">{{aplication.documentation}}</h6>
              </q-card-section>
            </q-card>
          </q-expansion-item>
          <q-expansion-item
            icon="cloud_download"
            label="Releases"
            header-class="text-orange"
            class="itemLabel"
          >
            <q-card class="bg-twitch">
              <q-card-section>
                <h6 style="color: #ffffff"> {{lastRelease}}</h6>
              </q-card-section>
            </q-card>
          </q-expansion-item>
        </q-list>
      </div>
    </div>
    <div class="row">
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-4 offset-xl-4 text-center text-orange">
        <h6 class="q-mb-xs">Escribe tu review</h6>
      </div>
    </div>
    <div class="row">
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-3 offset-xl-3">
        <q-input dark outlined bottom-slots v-model="email" type="email" label="Nombre" >
          <template v-slot:prepend>
            <q-icon name="perm_identity" />
          </template>
          <template v-slot:append>
            <q-icon name="close" @click="email = ''" class="cursor-pointer" />
          </template>
        </q-input>
      </div>
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-3">
        <q-input dark outlined bottom-slots v-model="email" type="email" label="Email" >
            <template v-slot:prepend>
              <q-icon name="mail" />
            </template>
            <template v-slot:append>
              <q-icon name="close" @click="email = ''" class="cursor-pointer" />
            </template>
          </q-input>
      </div>
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-6 offset-xl-3">
        <q-input
          dark 
          outlined
          v-model="text"
          type="textarea"
        />
      </div>
    </div>
    <div v-for="rating in ratings" class="row">
      <div class="q-pa-xs q-gutter-y-xs col-xs-12 col-sm-12 col-xl-6 offset-xl-3">
        <q-rating class="q-mb-xs q-mt-lg" 
        v-model="rating.rating"
        size="1em"
        readonly
        />
        <h6 class="q-pa-xs q-mt-xs q-mb-xs q-mr-xs" >{{rating.user.email}}</h6>
        <h6 class="q-pa-xs q-mt-xs q-mb-xs float-left" >"{{rating.comment}}"</h6> 
      </div>
    </div> 
  </div>
    <div v-else-if="aplication.published == false">
      <h6>Aplicación en proceso de revisión</h6>
    </div>

</template>


<script>

import Carousel from 'layouts/Carousel.vue'
import Card from 'layouts/Card.vue'
import { mapGetters } from 'vuex'
export default {
  name: 'PageIndex',
  components: {
    Carousel,
    Card
  },
  data () {
    return {
      tab: 'mails',
      email: '',
      text: '',
      approved: false,
      splitterModel: 20,
      ratingModel: 3,
      aplication: [],
      ratings: [],
      averageRating: 0,
      comment: '',
      completed: false,
      usercheck: [{role: 0}],
      lastRelease: '',
      releases: []
    }
  },
  computed: {
    ...mapGetters({ currentUser: 'currentUser' }),
    checkCurrentLogin () {
      if (!this.currentUser) {
        return false
      }
      else {
        console.log("logueado")
        return true
      }
    }
  },
  beforeRouteUpdate(to, from, next) {
    this.$axios.get("/api/v1/apps/"+this.$route.params.id+"/releases")
       .then(request => { this.releases = request.data 

          //this.autor = this.releases[0].author.login
          this.lastRelease = this.releases[0].zipball_url
          })
        .catch(() => { alert('Something went wrong!') })
    this.$axios.get("/api/v1/apps/"+to.params.id+"")
    .then(request => { this.aplication = request.data
      })
    .catch(() => { alert('DSADSA') })
    this.$axios.get("/api/v1/ratings/average/"+to.params.id+"")
    .then(request => { this.averageRating = parseFloat(request.data)
      })
    .catch(() => { alert('error average') })
    this.$axios.get("/api/v1/ratings/app/"+to.params.id+"")
      .then(request => { this.ratings = request.data                 
        })
      .catch(() => { alert('ERRORDSDSA') })  
      console.log('Updating slug from', to.params.id)
      next() 
      //make sure you always call next()
  },
  created () {
    this.$axios.get("/api/v1/apps/"+this.$route.params.id+"/releases")
       .then(request => { this.releases = request.data 

          //this.autor = this.releases[0].author.login
          this.lastRelease = this.releases[0].zipball_url
          })
        .catch(() => { alert('Something went wrong!') })
    this.$axios.get("/api/v1/apps/"+this.$route.params.id+"")
      .then(request => { this.aplication = request.data
        })
      .catch(() => { alert('Error app!') })
    this.$axios.get("/api/v1/ratings/average/"+this.$route.params.id+"")
      .then(request => { this.averageRating = parseFloat(request.data)
        })
      .catch(() => { alert('error average') })
    this.$axios.get("/api/v1/ratings/app/"+this.$route.params.id+"")
      .then(request => { this.ratings = request.data  
      console.log(this.rati)               
        })
      .catch(() => { alert('error rating') })
    if (this.currentUser) {
      this.$axios.get("/api/v1/apps/usercheck/"+this.currentUser.id+"/"+this.$route.params.id+"")
      .then(response => { 
        console.log(response.data)
        if (response.data.length == 0){
            console.log("NNNNNNNNNN")
        }
        else {
          console.log("ssssssssss")
          this.usercheck = response.data
        }
               
        })
      .catch(() => { alert('SSS!') }) 
    }

     
 
  },
  methods: {
    checkApp () {
      console.log("dsadsad")
      this.approved = true
      var data = {"app_id": this.$route.params.id, "user_id": this.currentUser.id, "comment": this.comment, "approved": this.approved}
      var json = JSON.stringify(data);
      this.$axios.post("/api/v1/apps/approve",json)
      .then(response => { 
        this.completed = true
      })
      .catch(error => {
          console.log("error")
        })
      
    }
  }

}
</script>

<style >
	.center {
	  margin: auto;
	  width: 90%;
	}
  .embed-container {
    position: relative;
    padding-bottom: 56.25%;
    height: 0;
  }
  .embed-container iframe {
      position: absolute;
      top:0;
      left: 0;
      width: 100%;
      height: 100%;
  }
  .q-list--dark, .q-item--dark {
    color: #fff;
    border-color: rgb(0, 217, 153);
  }
  .itemLabel {
    line-height: 1.2em !important;
    max-width: 100%;
    color: rgb(0, 217, 153);
    font-size: x-large;
  }
  .q-rating__icon {
    color: rgb(0, 217, 153)
  }
  .bg-twitch {
    background: #0f0e11 !important;
  }
  .q-list--bordered {
    border: 5px solid rgb(0, 217, 153);
  }
  
   

</style>