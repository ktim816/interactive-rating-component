<template>
  <div :class="[$style.wrapper]">
    <slot />
  </div>
</template>

<script setup lang="ts"></script>

<style lang="scss" module>
.wrapper {
  @apply sm:rounded-4xl rounded-[15px] w-full sm:max-w-[412px] max-w-[327px] bg-black-gradient;
}
</style>
