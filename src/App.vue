<template lang="jade">
#app()
  vsider
  vheader(:phone='phone')
  transition(name="slide-fade")
    router-view
  vfooter
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      phone: ''
    }
  },
  mounted () {
    const isLogin = localStorage.getItem('login')
    this.phone = localStorage.getItem('phone')
    if (isLogin !== 'true' && !isAllow(this)) {
      this.$router.push('/login')
    }
  }
}

function isAllow (_this) {
  return _this.$route.matched[0].path === '/html/:id'
}

</script>

<style lang="stylus">
$siderrWidth = 130px
$headerWidth = 60px

html, body
  width 100%
  height 100%
  margin 0
  padding 0
  overflow-x hidden

#app
  color #2c3e50
  background transparent
  height calc(100%)
  width 100%
  font-family Sans-serif

.admin
  width calc(100% - $siderrWidth)
  margin-left $siderrWidth
  height calc(100% - 120px)
  background white
  padding 30px
  padding-top 90px

  .form-inline
    top 12px
    position relative

#vsider .el-row
  position absolute
  bottom 0
  left 0
  width $siderrWidth
  height calc(100% - 60px)
  background-color #eef1f6
  position fixed
  overflow-y scroll
  z-index 2

  .el-col
    width 100%

#vsider .el-row::-webkit-scrollbar
  display none


#vheader
  height $headerWidth
  width 100%
  padding-right 30px
  background #eef1f6
  position fixed
  z-index 99999
  display block
  top 0
  left 0
  box-shadow 0px 2px 10px 3px rgba(0,0,0,0.15);

.title
  float left
  width 100%
  h1
    display inline-block
    margin-right 20px

.el-pagination
  text-align left
// 编辑器的 z-index 太高了
.el-notification
  top 70px !important
  z-index 99999 !important

.no-touch-bg
  user-select none
  -webkit-tap-highlight-color transparent
  -webkit-touch-callout none
  -webkit-user-select none

.a-title-text
  color #2c3e50
  font-size 2rem
  font-weight bold

.border1
  border 1px solid #D3D3D3
.pointer
  cursor pointer


.slide-fade-enter-active
  transition all .1s ease
.slide-fade-leave-active
  transition all .1s cubic-bezier(1.0, 0.5, 0.8, 1.0)
.slide-fade-enter, .slide-fade-leave-active
  transform translateX(10px)
  opacity 0

.el-row
  margin-bottom 20px
  &:last-child
    margin-bottom 0
.el-col
  border-radius 4px
  cursor pointer
.bg-purple-dark
  background #99a9bf
.bg-purple
  background #d3dce6
.bg-purple-light
  background #e5e9f2
.grid-content
  border-radius 4px
  min-height 46px
  padding 10px
  position relative
.center
  position   absolute
  top        50%
  left       50%
  transform  translate(-50%,-50%)
.row-bg
  padding 10px 0
  background-color #f9fafc
html
  font-size 62.5%
a
  text-decoration none
  cursor pointer
</style>
