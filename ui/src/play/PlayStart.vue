<template>
  <el-dialog v-if="dialogVisible" v-model="dialogVisible" :title="playItem.name" center>
    <div
        class="flex-center" style="width: 100%;max-height: 500px;min-height: 200px;">
      <Artplayer :src="src" :subtitles="subtitles"/>
    </div>
  </el-dialog>
</template>
<script setup>

import {ref} from "vue";
import Artplayer from "./Artplayer.vue";

let dialogVisible = ref(false)
let src = ref('')
let ani = ref({})
let playItem = ref()
let subtitles = ref([])

let show = (i, pi) => {
  src.value = `api/files?filename=${pi.filename}&s=${window.authorization}`
  for (let subtitle of pi.subtitles) {
    subtitle.url = `api/files?filename=${subtitle.url}&s=${window.authorization}`
  }
  subtitles = pi.subtitles
  ani.value = i
  playItem.value = pi
  dialogVisible.value = true
}

defineExpose({
  show
})
</script>
