<template>
  <div
    class="p-12 h-full flex flex-col flex-grow min-h-[100vh]">
    <!-- <CommonButton>publish now</CommonButton> -->
    <div
      id="vditor"
      ref="vditorRef" />
  </div>
</template>

<script lang="ts" setup>
  import Vditor from 'vditor';
  import 'vditor/dist/index.css';

  const vditorRef = ref<Vditor | null>(null);

  onMounted(() => {
    vditorRef.value = new Vditor('vditor', {
      placeholder: '',
      after: () => {
        vditorRef.value?.setValue('');
      },
    });
  });
</script>

<style scoped lang="scss">
  #vditor {
    height: 100% !important;
    flex-grow: 1;
  }
</style>
