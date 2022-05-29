<template>
  <div>
    <PostView v-for="(instar, i) in instardata" :key="i" :instar=instar />
  </div>
</template>

<script>

import PostView from './PostView.vue'

export default {
  name: 'ContainerView',
  props: {
    instardata : Array
  },
  components : {
    PostView : PostView
  }
  
}
</script>


<style>

</style>
