<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          icon="menu"
          aria-label="Menu"
        />

      </q-toolbar>
       <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">Todo</div>
        <div class="text-subtitle1">What's your tasks today?</div>
        <div class="text-subtitle1">{{ todayDt }}</div>
    </div>
    <q-img 
      class="svg-testheader absolute-top" 
      src="statics/wave.svg"
    />
    </q-header>
   
    <q-drawer
      v-model="leftDrawerOpen"
      bordered
      content-class="bg-grey-2"
    >
     <q-list>
        <q-item-label header>Menu</q-item-label>
       
        <q-item
          to="/"
          exact
          clickable
          v-ripple
        >
          <q-item-section avatar>
            <q-icon name="home" />
          </q-item-section>
          <q-item-section>
            <q-item-label>Todo</q-item-label>
            <q-item-label caption>Main Page</q-item-label>
          </q-item-section>
        </q-item>

        <q-item
          to="/help"
          exact
          clickable
          v-ripple
        >
          <q-item-section avatar>
            <q-icon name="help" />
          </q-item-section>
          <q-item-section>
            <q-item-label>Help</q-item-label>
            <q-item-label caption>About project</q-item-label>
          </q-item-section>
        </q-item>
        
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from 'quasar'

export default {
  name: 'MyLayout',

  data () {
    return {
      leftDrawerOpen: false
    }
  },
  computed: {
    todayDt() {
      let timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd D MMMM')
    }
  }
}
</script>

<style lang="scss">
  .svg-testheader {
    height: 40vh;
    z-index: -1;
  }
  .q-header {
    margin-bottom: 15%;
  }
  @media screen and(max-width: 455px){
    .svg-testheader {
      height: 70vh;
    }
  }
</style>