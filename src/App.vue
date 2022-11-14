<template>
  <router-view />
</template>

<script setup lang="ts">
  import debug from '@/utils/debug';
  import watermark from '@/utils/lib/watermark';
  import copyPaste from '@/utils/lib/copy-paste';

  onMounted(() => {
    // 因为debug是存入localStorage中的，刷新页面会从localStorage取出，根据debug控制是否隐藏
    debug.init();

    // const { username = '', mobile = '' } = auth.getUser();
    const user = { username: 'wythe', mobile: '156****8180' };
    watermark.add({
      content: user.username + ' ' + user.mobile,
    });
    copyPaste.disable();
  });

  onBeforeUnmount(() => {
    watermark.remove();
    copyPaste.enable();
  });
</script>

<style>
  #app {
    font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
    font-synthesis: none;
    text-rendering: optimizeLegibility;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    -webkit-text-size-adjust: 100%;
  }
</style>
