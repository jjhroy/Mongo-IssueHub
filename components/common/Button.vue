<template>
  <button class="mongo-btn">
    <slot></slot>
  </button>
</template>
<style scoped lang="postcss">
  .mongo-btn {
    @apply inline-block 
    whitespace-nowrap 
    text-sm 
    h-8
    bg-[#1677ff] 
    text-[#fff] 
    shadow-[0_2px_0_rgba(5,145,255,0.1)] 
    text-center 
    max-w-max 
    px-4 
    py-1 
    rounded-md 
    outline-none
    hover:bg-[#4096ff]
    active:bg-[#0958d9];
  }
</style>
