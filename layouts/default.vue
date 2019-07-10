<template>
  <v-app :dark="isDark">
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      isDark: false,
      items: [
        {
          icon: 'apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'bubble_chart',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  },
  methods: {
    konami(callback) {
      let kkeys = [];
      // up,up,down,down,left,right,left,right,B,A
      const konami = '38,38,40,40,37,39,37,39,66,65';
      return event => {
        kkeys.push(event.keyCode);
        if (kkeys.toString().indexOf(konami) >= 0) {
          callback();
          kkeys = [];
        }
      };
    }
  },
  created: function () {
    const handler = this.konami(() => {
      this.isDark = !this.isDark;
    });
    window.addEventListener('keydown', handler);
  }
}
</script>
