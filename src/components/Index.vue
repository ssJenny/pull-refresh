<template>
  <div class="wrapper" ref="wrapper">
    <scroller :on-infinite="infinite" :on-refresh="refresh" ref="myscroll">
      <ul class="content">
        <li v-for="item in data">
          {{item}}
        </li>
      </ul>
    </scroller>
  </div>
</template>

<script>

  import Vue from 'vue'
  import VueScroller from 'vue-scroller'
  Vue.use(VueScroller)
export default {
  data () {
    return {
      data:[],
      noData:''
    }
  },
  created() {
    this.loadData()
  },
  mounted() {
    this.top = 1
  },
  methods: {
    loadData() {
      var max = parseInt(Math.random() * 20 + 10)
      for(let i = 0; i <=max ; i++) {
        this.data.push(i)
      }
    },
    infinite(done){
      if(this.noData) {
        setTimeout(() => {
          this.$refs.myscroll.finishInfinite(2);
        })
        return;
      }
      let self = this;
      let start = this.data.length;

      setTimeout( () => {
        for(let i = start + 1; i < start + 10; i++){
          self.data.push(i)
        }
        if(start >  30){
          self.noData = "没有更多数据"
        }

        self.$refs.myscroll.resize();

        done()
      }, 1500)
    },
    refresh(done) {
      console.log('refresh')
      setTimeout(() => {
        let start = this.top - 1
        for(let i = start; i > start - 10; i--) {
          this.data.splice(0,0, i)
        }
        this.top = this.top - 10;
        done()
      }, 1500)
    }
  },


  components: {
    BScroll,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  ul{
    list-style: none;
  }
  li{
    height: 6rem;
    line-height: 6rem;
    border-bottom: 1px solid #ccc;
  }
</style>
