<template>
  <v-container class="ma-0 pa-0" grid-list-sm>
    <div class="text-right">
      <v-btn small text to="/blogs" class="blue--text">
        All Blogs <v-icon>mdi-chevron-right</v-icon>
      </v-btn>
    </div>
    <v-layout wrap>
      <blog-item-component  v-for="blog in blogs" :key="`blog-`+blog.id" :blog="blog"></blog-item-component>
    </v-layout>

    <!-- <button @click="action_tambah(10)">Tambah</button> -->
    <button @click="action_tambah(10)">Tambah</button>
    {{ count }}
  </v-container>
</template>

<script>
import BlogItemComponentVue from '../components/BlogItemComponent.vue';
import { mapMutations, mapGetters } from 'vuex'
    export default{
        data: () => ({
            apiDomain : 'http://demo-api-vue.sanbercloud.com' ,
            blogs : [],
        }),
        components : {
          'blog-item-component' : BlogItemComponentVue
        },
        computed: {
          // Kirim ke Vuext

          // Cara 1
          // count(){
          //   return this.$store.getters.count
          // }

          /// Cara 2
          ...mapGetters({
            'count' : 'counter/count'
          })
        },
        methods: {
          go(){
              const config = {
              method : 'get',
              url : this.apiDomain + '/api/v2/blog/random/4'
            }

            this.axios(config)
            .then(response => {
              let { blogs } = response.data;
              this.blogs = blogs;
            }).catch( error => {
              console.log(error)
            });
          },
          // Kirim ke Vuext
          // Cara 1
          // action_tambah(payload){
          //   this.$store.commit('increment', payload)
          // }

          // Cara 2
          ...mapMutations({
            'action_tambah' : 'counter/increment'
          })
        },
        created(){

          this.go()
        }
    }
</script>
