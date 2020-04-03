<template>
  <div>
    <div class="row">
      <div class="col-xl-5 offset-xl-1">
        <q-card class="my-card">
          <img src="https://i.imgur.com/MR3wXhi.png" style="max-height: 400px">
          <q-list>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="amber" name="code" />
              </q-item-section>
              <q-item-section>
                <q-item-label style="color: black;">SDK </q-item-label>
                <q-item-label caption>Windows</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="primary" name="perm_identity" />
              </q-item-section>
              <q-item-section>
                <q-item-label style="color: black;">Contribuciones</q-item-label>
                <q-item-label caption></q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="red" name="calendar_today" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">Año</q-item-label>
                <q-item-label caption>2017</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
          <q-tabs v-model="tab" class="text-teal">
            <q-tab label="Código fuente" name="one" />
            <q-tab label="Documentación" name="two" />
          </q-tabs>
          <q-separator/>
          <q-tab-panels v-model="tab" animated>
            <q-tab-panel name="one" style="color: black">
              https://github.com/Open-Glove/SDK-OpenGlove
            </q-tab-panel>

            <q-tab-panel name="two" style="color: black">
              SDK para facilitar el desarrollo de aplicaciones para OpenGlove
            </q-tab-panel>
          </q-tab-panels>
        </q-card>
      </div>
      <div class="col-xl-5">
        <q-card class="my-card">
          <img src="https://i.imgur.com/Ug67n3A.png" style="max-height: 400px">
          <q-list>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="amber" name="code" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">SDK </q-item-label>
                <q-item-label caption>Android</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="primary" name="perm_identity" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">Contribuciones</q-item-label>
                <q-item-label caption></q-item-label>
              </q-item-section>
            </q-item>

            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="red" name="calendar_today" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">Año</q-item-label>
                <q-item-label caption>2017</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
          <q-tabs v-model="tabAndroid" class="text-teal">
        <q-tab label="Código fuente" name="oneAndroid" />
        <q-tab label="Documentación" name="twoAndroid" />
      </q-tabs>

      <q-separator />

      <q-tab-panels v-model="tabAndroid" animated>
        <q-tab-panel name="oneAndroid" style="color: black">
          https://github.com/Open-Glove/OpenGloveApp
        </q-tab-panel>

        <q-tab-panel name="twoAndroid" style="color: black">
          With so much content to display at once, and often so little screen real-estate,
          Cards have fast become the design pattern of choice for many companies, including
          the likes of Google and Twitter.
        </q-tab-panel>
      </q-tab-panels>
        </q-card>
      </div>
    </div>
    
    
  
  
  <div class="row">
    <div class="col-xs-12 col-sm-6 col-md-4 col-lg-2 offset-lg-3">
      <div class="q-pa-md q-gutter-md">
        <q-card class="my-card">
          <img src="https://i.imgur.com/OaHf6we.png">
          <q-list>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="amber" name="code" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">API </q-item-label>
                <q-item-label caption>C#</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="primary" name="perm_identity" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">Autor</q-item-label>
                <q-item-label caption>Rodrigo Andrés Monsalve Lagos</q-item-label>
              </q-item-section>
            </q-item>

            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="red" name="calendar_today" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">Año</q-item-label>
                <q-item-label caption>2015</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-card>
        <div class="q-pa-sm" style="max-width: 600px; padding-top: 0px;  margin-top: 0px">
          <q-list bordered class="rounded-borders" style="background: white; color: black;">
            <q-expansion-item
              expand-separator
              icon="code"
              label="Código fuente"
              caption="Github"
            >
              <q-card>
                <q-card-section>
                  <a href="https://github.com/Open-Glove/OpenGlove-API-C-Sharp">https://github.com/Open-Glove/OpenGlove-API-C-Sharp</a>
                  
                </q-card-section>
              </q-card>
            </q-expansion-item>

            <q-expansion-item
              expand-separator
              icon="library_books"
              label="Documentación"
              header-class="text-primary"
              caption="PDF"

            >
              <q-card>
                <q-card-section>
                  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quidem, eius reprehenderit eos corrupti
                  commodi magni quaerat ex numquam, dolorum officiis modi facere maiores architecto suscipit iste
                  eveniet doloribus ullam aliquid.
                </q-card-section>
              </q-card>
            </q-expansion-item>
          </q-list>
        </div>
      </div>
    </div>
    <div class="col-xs-12 col-sm-6 col-md-4 col-lg-2">
      <div class="q-pa-md q-gutter-md">
        <q-card class="my-card">
          <img src="https://i.imgur.com/qz9r4O4.png">
          <q-list>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="amber" name="code" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">API </q-item-label>
                <q-item-label caption>Java</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="primary" name="perm_identity" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">Autor</q-item-label>
                <q-item-label caption>Rodrigo Andrés Monsalve Lagos</q-item-label>
              </q-item-section>
            </q-item>

            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="red" name="calendar_today" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">Año</q-item-label>
                <q-item-label caption>2015</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-card>
        <div class="q-pa-sm" style="max-width: 600px; padding-top: 0px;  margin-top: 0px">
          <q-list bordered class="rounded-borders" style="background: white; color: black;">
            <q-expansion-item
              expand-separator
              icon="code"
              label="Código fuente"
              caption="Github"
            >
              <q-card>
                <q-card-section>
                   <a href=https://github.com/Open-Glove/OpenGlove-API-JAVA>https://github.com/Open-Glove/OpenGlove-API-JAVA</a>
                </q-card-section>
              </q-card>
            </q-expansion-item>

            <q-expansion-item
              expand-separator
              icon="library_books"
              label="Documentación"
              header-class="text-primary"
              caption="PDF"

            >
              <q-card>
                <q-card-section>
                  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quidem, eius reprehenderit eos corrupti
                  commodi magni quaerat ex numquam, dolorum officiis modi facere maiores architecto suscipit iste
                  eveniet doloribus ullam aliquid.
                </q-card-section>
              </q-card>
            </q-expansion-item>
          </q-list>
        </div>
      </div>
    </div>
    <div class="col-xs-12 col-sm-6 col-md-4 col-lg-2">
      <div class="q-pa-md q-gutter-md">
        <q-card class="my-card">
          <img src="https://i.imgur.com/zMR024h.png">
          <q-list>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="amber" name="code" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">API </q-item-label>
                <q-item-label caption>JavaScript</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="primary" name="perm_identity" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">Autor</q-item-label>
                <q-item-label caption>Rodrigo Andrés Monsalve Lagos</q-item-label>
              </q-item-section>
            </q-item>

            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="red" name="calendar_today" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">Año</q-item-label>
                <q-item-label caption>2015</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-card>
        <div class="q-pa-sm" style="max-width: 600px; padding-top: 0px;  margin-top: 0px">
          <q-list bordered class="rounded-borders" style="background: white; color: black;">
            <q-expansion-item
              expand-separator
              icon="code"
              label="Código fuente"
              caption="Github"
            >
              <q-card>
                <q-card-section>
                  <a href=https://github.com/Open-Glove/OpenGlove-API-JavaScript>https://github.com/Open-Glove/OpenGlove-API-JavaScript</a>
                </q-card-section>
              </q-card>
            </q-expansion-item>

            <q-expansion-item
              expand-separator
              icon="library_books"
              label="Documentación"
              header-class="text-primary"
              caption="PDF"

            >
              <q-card>
                <q-card-section>
                  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quidem, eius reprehenderit eos corrupti
                  commodi magni quaerat ex numquam, dolorum officiis modi facere maiores architecto suscipit iste
                  eveniet doloribus ullam aliquid.
                </q-card-section>
              </q-card>
            </q-expansion-item>
          </q-list>
        </div>
      </div>
    </div>
  </div>
  <div class="row">
    <div class="col-xs-12 col-sm-6 col-md-4 col-lg-4 offset-lg-4">
      <div class="q-pa-md q-gutter-md">
        <q-card class="my-card">
          <img src="https://i.imgur.com/kqiLyvy.png">
          <q-list>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="amber" name="code" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">Arduino </q-item-label>
                <q-item-label caption>C++</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="primary" name="perm_identity" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">Autor</q-item-label>
                <q-item-label caption>Rodrigo Andrés Monsalve Lagos</q-item-label>
              </q-item-section>
            </q-item>

            <q-item clickable>
              <q-item-section avatar>
                <q-icon color="red" name="calendar_today" />
              </q-item-section>

              <q-item-section>
                <q-item-label style="color: black;">Año</q-item-label>
                <q-item-label caption>2015</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-card>
        <div class="q-pa-sm" style="max-width: 600px; padding-top: 0px;  margin-top: 0px">
          <q-list bordered class="rounded-borders" style="background: white; color: black;">
            <q-expansion-item
              expand-separator
              icon="code"
              label="Código fuente"
              caption="Github"
            >
              <q-card>
                <q-card-section>
                  <a href=https://github.com/Open-Glove/OpenGlove-API-JavaScript>https://github.com/Open-Glove/OpenGlove-API-JavaScript</a>
                </q-card-section>
              </q-card>
            </q-expansion-item>

            <q-expansion-item
              expand-separator
              icon="library_books"
              label="Documentación"
              header-class="text-primary"
              caption="PDF"

            >
              <q-card>
                <q-card-section>
                  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quidem, eius reprehenderit eos corrupti
                  commodi magni quaerat ex numquam, dolorum officiis modi facere maiores architecto suscipit iste
                  eveniet doloribus ullam aliquid.
                </q-card-section>
              </q-card>
            </q-expansion-item>
          </q-list>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  data () {
    return {
      stars: 4,
      slide: 'first',
      tab: 'one',
      tabAndroid: 'oneAndroid'
    }
  }
}
</script>

<style type="text/css">
  .custom-caption{
  text-align: center;
  padding: 12px;
  color: white;
  background-color: rgba(0, 0, 0, .3);}

</style>