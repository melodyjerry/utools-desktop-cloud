<template>
  <Window :uuid='uuid' :startpos_x="startpos_x" :startpos_y="startpos_y" :zindex="zindex" :blacktheme="true"  :minimized="minimized" @resize_start="show_blocker=true" @resize_end="show_blocker=false">
    <template v-slot:header>
      <div class="tw-flex tw-items-center tw-select-none" style="pointer-events:none;"> 
        <img src="../../assets/images/icons/music.png" alt="" style="pointer-events:auto;" class=" tw-w-8 tw-h-7 tw-ml-4">
        <div class=" tw-ml-4 tw-font-bold tw-tracking-wider tw-w-14" style="pointer-events:auto;"> Music </div>
      </div>
    </template>
    <template v-slot:content>
      <div class="tw-w-full tw-h-full tw-flex tw-overflow-hidden" @click="go_focus">
        <iframe src="https://netease-music.fe-mm.com/#/music/playlist" frameborder="0" class="zoomined-frame "></iframe>
        <div class="tw-w-full tw-h-full tw-absolute background-color" style="top:0" v-if="show_blocker">
          <span class="tw-hidden"> this div is to prevent iframe take control over mouse event </span>
        </div>
      </div>
    </template>
  </Window>
</template>

<script>
import Window from '../WindowBasic/Window.vue'
// import Aplayer from 'vue-aplayer'

export default {
  name: 'WindowMusic',
  components: {
    Window
  },
  data(){
    return {
      show_blocker: false,
    }
  },
  props:{
    uuid:String,
    startpos_x:{
      default:60,
    },
    startpos_y:{
      default:60
    },
    zindex:{
      type:Number,
      default:999,
    },
    minimized:{
      type:Boolean,
      default:false,
    },
    default_width:{
      type:Number,
      default:-1
    },
    default_height:{
      type:Number,
      default:-1
    },
    fixedsize:{
      type:Boolean,
      default:false,
    }
  },
  created(){
    // this.$axios.raw('musics.json')
    // .then((res) => {
    //   document.body.style.cursor='normal'
    //   if (typeof(res.data) === 'string') {
    //     // error
    //     console.log("Load error, got string returned")
    //   }
    //   this.musiclist = res.data
    // })
    // .catch((err) => {
    //   console.log("[WindowMusic] axios error: ", err)
    // })
  },
  mounted(){
    
  },
  watch:{
  },
  computed:{
    // firstmusic(){
    //   if (this.musiclist.length > 0) {
    //     return this.musiclist[0]
    //   } else {
    //     return {
    //       title: '',
    //       artist: '',
    //       src: '',
    //       pic: '',
    //     }
    //   }
    // }
  },
  methods:{
    window_height_changed(val){
      this.cont_height = val - this.cont_margin
    },
    mr_clicked(){
      this.$store.commit('show_context_menu')
    },
     go_focus(){
      this.$store.commit('refresh_window_focus', {'type':'music'})
    },
  }
}
</script>

<style scoped>
.zoomined-frame{
  /* width: 80% !important;
  height: 80% !important;
  -webkit-transform: scale(1.25);
  transform: scale(1.25);
  -webkit-transform-origin: 0 0;
  transform-origin: 0 0; */
  width: 100%;
  height: 100%;
}
</style>
