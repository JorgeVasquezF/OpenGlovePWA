<template>
  <q-layout view="hHh lpR fFf" class="bg-twitch text-white">
    <q-header elevated class="bg-primary text-white q-gutter-y-md" height-hint="98">
      <q-toolbar>
        <!--<q-btn dense flat round icon="menu" @click="left = !left" /> !-->
        <q-toolbar-title >
          <q-avatar>
            <img src="https://i.imgur.com/20FU3lI.png">
          </q-avatar>
          OpenGlove
        </q-toolbar-title>
        <multiselect class="gt-sm" style="max-width: 400px" v-model="selectedCountries" id="ajax" label="name" track-by="code" placeholder="Tipea para buscar" open-direction="bottom" :options="countries" :multiple="true" :searchable="true" :loading="isLoading" :internal-search="false" :clear-on-select="false" :close-on-select="false" :options-limit="300" :limit="3" :limit-text="limitText" :max-height="600" :show-no-results="false" :hide-selected="true" @search-change="asyncFind" @select="onSelectSearch" @remove="remove">
                          
          <template slot="clear" slot-scope="props">
            <div class="multiselect__clear" v-if="selectedCountries.length" @mousedown.prevent.stop="clearAll(props.search)"></div>
          </template><span slot="noResult">Oops! No elements found. Consider changing the search query.</span>
        </multiselect>
        <!-- MENU DE BARRA PARA ESCRITORIO !-->
        <q-tabs align="center" class="gt-xs">
          <q-route-tab to="/" label="Home" icon="home" />
          <q-route-tab to="/store" label="Store" icon="store" />
          <q-route-tab to="/tool" label="Tools" icon="build"/>
          <q-route-tab class="text-black" v-if="currentUser" to="/upload" label="Up App" icon="cloud_upload"/>
        </q-tabs>
        <!-- BOTONES DE MENU PARA ESCRITORIO !--> 
          <div class="q-pa-md q-gutter-sm gt-xs">
            <template v-if="!currentUser">
              <q-btn style="background: #424242 ; color: white" label="Iniciar Sesión" @click="login = true"/>
              <q-btn style="color: white" color="deep-orange" label="Registarse" @click="register = true"/>
            </template>
            <template v-if="currentUser">
              <q-btn style="color: white" color="deep-orange" label="Salir" @click="logout()"/>
            </template>
          </div>
        <!-- BOTONES DE MENU PARA MOBILE !-->   
        <div class="q-pa-md q-gutter-sm lt-sm" >
          <template v-if="!currentUser">
            <q-btn id="login"
              round
              dense
              color=#0f0e11
              size=sm
              icon="input"
              @click="login = true"
            />
            <q-btn dense size=sm style="color: white" color="deep-orange" label="Registrarse" />
          </template>
          <template v-if="currentUser">
              <q-btn style="color: white" color="deep-orange" label="Salir" @click="logout()"/>
          </template>
        </div>
      </q-toolbar>
      <!-- MENU DE BARRA PARA MOBILE !-->
      <q-tabs  align="center" class="lt-sm" style="margin-top: 0px;">
          <q-route-tab to="/" label="Home" icon="home"/>
          <q-route-tab to="/store" label="Store" icon="store"/>
          <q-route-tab to="/tool" label="Tools" icon="build"/>
          <q-route-tab v-if="currentUser" to="/upload" label="Up App" icon="cloud_upload"/>
      </q-tabs>
      
        <multiselect class="lt-md center" style="max-width: 400px; margin-bottom: 5px;" v-model="selectedCountries" id="ajax" label="name" track-by="code" placeholder="Tipea para buscar" open-direction="bottom" :options="countries" :multiple="true" :searchable="true" :loading="isLoading" :internal-search="false" :clear-on-select="false" :close-on-select="false" :options-limit="300" :limit="3" :limit-text="limitText" :max-height="600" :show-no-results="false" :hide-selected="true" @search-change="asyncFind" @select="onSelectSearch" @remove="remove">
                          
          <template slot="clear" slot-scope="props">
            <div class="multiselect__clear" v-if="selectedCountries.length" @mousedown.prevent.stop="clearAll(props.search)"></div>
          </template><span slot="noResult">Oops! No elements found. Consider changing the search query.</span>
        </multiselect>
     
    </q-header>
    <q-drawer v-model="left" side="left" overlay behavior="desktop" elevated>
      <!-- drawer content -->
    </q-drawer>
    <!-- DIALOG LOGIN -->
    <q-dialog v-model="login">
      <q-card style="width: 700px; max-width: 80vw; color: #00d999" class="bg-twitch">
        <q-card-section>
          <div class="text-h6 text-center">Inicia sesión</div>
        </q-card-section>
        <q-card-section>
          <q-input dark outlined bottom-slots v-model="email" type="email" label="Email" >
            <template v-slot:prepend>
              <q-icon name="mail" />
            </template>
            <template v-slot:append>
              <q-icon name="close" @click="email = ''" class="cursor-pointer" />
            </template>
          </q-input>
          <q-input dark outlined bottom-slots v-model="password" label="Password" :type="!isPwd ? 'password' : 'text'" >
            <template v-slot:prepend>
              <q-icon name="vpn_key" />
            </template>
            <template v-slot:append>
              <q-icon
                :name="isPwd ? 'visibility' : 'visibility_off'"
                class="cursor-pointer"
                @click="isPwd = !isPwd"
              />
            </template>
          </q-input>
        </q-card-section>
        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" @click="loginUser()" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
    <!-- DIALOG REGISTER -->
    <q-dialog v-model="register">
      <q-card style="width: 700px; max-width: 80vw; color: #00d999" class="bg-twitch">
        <q-card-section>
          <div class="text-h6 text-center">Registrate</div>
        </q-card-section>
        <q-card-section>
          <q-form
          
            class="q-gutter-xs"
          >
            <q-input
              dark
              bottom-slots
              outlined
              v-model.trim="$v.username.$model"
              label="Username *"
              error-message="Username debe tener al menos 4 carácteres"
              :error="!$v.username.minLength"

            >
              <template v-slot:prepend>
                  <q-icon name="perm_identity" />
              </template>
             
            </q-input>
            <q-input
              dark
              bottom-slots
              outlined
              type="email"
              v-model="$v.emailRegister.$model"
              label="Email *"
              error-message="example@example.cl"
              :error="!$v.emailRegister.email"
            >
              <template v-slot:prepend>
                  <q-icon name="email" />
              </template>
            </q-input>
            <q-input 
              dark 
              outlined 
              bottom-slots 
              v-model="passwordRegister" 
              label="Password"
              :type="!isPwdRegister ? 'password' : 'text'" >
              <template v-slot:prepend>
                <q-icon name="vpn_key" />
              </template>
              <template v-slot:append>
                <q-icon
                  :name="isPwdRegister ? 'visibility' : 'visibility_off'"
                  class="cursor-pointer"
                  @click="isPwdRegister = !isPwdRegister"
                />
              </template>
            </q-input>
      
          </q-form>
        </q-card-section>
        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" @click="registerUser()"/>
          <q-btn flat label="Cancelar" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
    <q-dialog v-model="registerComplete">
      <q-card style="width: 700px; max-width: 80vw; color: #00d999" class="bg-twitch">
        <q-card-section>
          <div class="text-h6 text-center">Registro completo</div>
        </q-card-section>
        <q-card-actions align="right">
          <q-btn flat label="Ok" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>  
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import Multiselect from 'vue-multiselect'
import { mapGetters } from 'vuex'
import { required, minLength, between, email, sameAs } from 'vuelidate/lib/validators'  
export default {
  data () {
    return {
      position: 'top',
      left: false,
      registerComplete: false,
      username: '',
      emailRegister: '',
      passwordRegister: '',
      isPwdRegister: '',
      email: '',
      password: '',
      isPwd: '',
      login: false,
      register: false,
      busqueda: 0,
      countries: [],
      selectedCountries: [],
      isLoading: false,
    }
  },
  components: {
    Multiselect
  },
  validations: {
    username: {
      required,
      minLength: minLength(4)
    },
    emailRegister: {
      required,
      email
    }
  },
  computed: {
    ...mapGetters({ currentUser: 'currentUser' })
  },
  methods: {
    loginUser () {
      this.$axios.post('/api/v1/auth', { user: this.email, password: this.password })
      .then(request => this.loginSuccessful(request))
      .catch(() => this.loginFailed())
      
    },
    registerUser () {
      this.$axios.post('/api/v1/users', { username: this.username, email: this.emailRegister, password: this.passwordRegister })
      .then(response => {
        this.register = false
        this.registerComplete = true
                       } )
      .catch(error => {
              console.log("error")
          })
      
    },
    loginSuccessful (req) {
      if (!req.data.token) {
        this.loginFailed()
        return
      }
      this.error = false
      localStorage.token = req.data.token
      this.$router.push(this.$route.path)
      location.reload(true)
    },
    loginFailed () {
      this.error = 'Login failed!'
      delete localStorage.token
    },
    logout () {
      delete localStorage.token
      location.reload(true)
    },
    asyncFind (query) {
      this.isLoading = true
      var data = {"name": query}
      var json = JSON.stringify(data);
      this.$axios.post("/api/v1/apps/search",json)
      .then(response => {
        this.countries = Object.values(response.data)
        this.isLoading = false
      })
      .catch(() => { alert('Error carga busqueda') })
    },
    onSelectSearch (option) {
      console.log(option)
      console.log(this.selectedCountries)
      this.$router.push({ path: `/aplication/${option.id}` });
     //location.reload(true)
    },
    
    remove () {
      this.busqueda = 0
      },
    limitText (count) {
      return `and ${count} other countries`
    },
  }
}
</script>

<style>
.bg-twitch {
    background: #0f0e11 !important;
}
#login {
  background: #0f0e11;
}

.center {
    margin: auto;
    width: 90%;
    padding-top: 4px;
  }

</style>

<style scoped>

.q-icon {
  color: #00d999;
}
.q-field__label {
  color: #00d999;
  }
  
</style>

<style src="vue-multiselect/dist/vue-multiselect.min.css">

</style>