<template>
  <div class="container" v-if="state">
    <v-spinner v-if="state === 'loading'" />
    <div v-if="state === 'ended' || isEnd" class="ended">已经全部加载完毕</div>
    <!-- <InfiniteScroll :load="loadData" ref="infiniteScroll"/> -->
  </div>
</template>

<script>
  import VSpinner from './Spinner.vue'

  export default {
    props: {
      load: {
        type: Function
      },
      isEnd: {
        type: Boolean,
        default: false
      }
    },

    data: () => ({
      state: ''
    }),

    components: { VSpinner },

    mounted() {
      this.onscroll = () => {
        if (this.isEnd) {
          this.state = 'ended'
        }
        if (this.state) return
        const scrollTopVal = window.pageYOffset || document.body.scrollTop || document.documentElement.scrollTop
        if ((document.body.scrollHeight - scrollTopVal < window.screen.height * 2) && scrollTopVal > 0) {
          this.state = 'loading'
          this.load().then(state => {
            if (state === 'ended' || this.isEnd) {
              this.state = 'ended'
            } else {
              this.state = ''
            }
          })
        }
      }

      window.addEventListener('scroll', this.onscroll, { passive: true })
    },

    destroyed() {
      window.removeEventListener('scroll', this.onscroll, { passive: true })
    },

    methods: {
      reset() {
        this.state = ''
      },

      end() {
        this.state = 'ended'
      }
    }
  }
</script>

<style lang="scss" scoped>
  .container {
    height: 60px;
    text-align: center;
    padding: 18px;
    background: #fff;
  }

  .ended {
    font-size: 14px;
    line-height: 24px;
    color: #b7b7b5;
  }
</style>
