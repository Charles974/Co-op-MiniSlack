<template>

  <div>

    <nav-bar></nav-bar>

    <section class="section coop-accueil">

          <div class="panel">

          <p class="panel-heading">
            Membres ({{ liste.length }} membre(s))
          </p>

          <member v-for="unMembre in liste" :memb="unMembre"></member>
        </div>
    </section>

  </div>

</template>

<script>

import NavBar from './navBar.vue'
import Member from './member.vue'

export default {
  name: 'MembersListe',
  components: {NavBar, Member},
  data () {
    return {
      liste : [],
      unMembre: '',
    }
  },
  mounted() {
    window.axios.get('members').then((response) => {
      this.liste = response.data;
    }).catch((error) => {
    });

    window.bus.$on('updateMember',() => {
      window.axios.get('members').then((response) => {
        this.liste = response.data;
      }).catch((error) => {
      });
    });

  }
}
</script>
