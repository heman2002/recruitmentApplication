<template>
  <q-layout>
    <div slot="header" class="toolbar">
      <q-toolbar-title :padding="1">
        Internship Application
      </q-toolbar-title>
      <button @click="drawerOpen()">
        <i>assignment</i>
      </button>
    </div>

    <q-tabs slot="navigation">
     <q-tab icon="view_quilt" route="/index" exact replace>Home</q-tab>
     <q-tab icon="view_day" route="/education" replace>Education</q-tab>
     <q-tab icon="view_day" route="/details" replace>Details</q-tab>
    </q-tabs>

    <router-view class="layout-view"></router-view>


    <q-drawer right-side swipe-only ref="rightDrawer">
      <div class="toolbar light">
        <q-toolbar-title :padding="1">
            Resume
        </q-toolbar-title>
      </div>



      </div>
    </q-drawer>

    <div slot="footer" class="toolbar">
      <div class="auto flex justify-center within-iframe-hide">
        <button v-go-back="'/showcase'">
          <i class="on-left animate-blink">
            replay
          </i>
          Back to Showcase
        </button>
      </div>
      <q-toolbar-title :padding="0" class="within-iframe-only">
        Footer
      </q-toolbar-title>
    </div>
  </q-layout>
</template>
