<template>
  <!-- 当插入插槽的元素需要添加属性时，可以给插槽外部添加div元素，
  往div元素中添加属性，确保属性能够添加到元素上去，而不会被替换掉 -->
  <div class="tab-bar-item" @click="btnClick">
    <div v-if="!isActive">
      <slot name="item-icon"></slot>
    </div>
    <div v-else>
      <slot name="item-icon-active"></slot>
    </div>
    <div :class="{ active: isActive }" :style="activeStyle">
      <slot name="item-text"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TabBarItem',
  props: {
    path: {
      type: String
    },
    activeColor: {
      type: String,
      default: 'red'
    }
  },
  data() {
    return {
      // isActive: false,
    }
  },
  computed: {
    isActive() {
      // 当前活跃的路由中所包含的路径是否匹配，匹配则isActive为true
      // /home -> $route.path(home)
      // /home -> $route.path(category)
      return this.$route.path.indexOf(this.path) !== -1
    },
    activeStyle(){
      return this.isActive ? {color: this.activeColor} : {}
    }
  },
  methods: {
    btnClick() {
      this.$router.replace(this.path).catch(err => {
        
      })
    }
  }
}
</script>

<style>
.tab-bar-item {
  flex: 1;
  text-align: center;
  height: 49px;
  font-size: 12px;
}
.tab-bar-item img {
  width: 24px;
  height: 24px;
  margin-top: 3px;
  vertical-align: middle;
  margin-bottom: 2px;
}
.active {
  color: red;
}
</style>
