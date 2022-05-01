<template>
  <modal-wrapper :class="[$style.wrapper]">
    <div :class="[$style.image]">
      <img :src="illustrationThankYou" />
    </div>
    <div
      v-if="typeof props.selectedScore === 'number'"
      :class="[$style.result]"
    >
      You selected {{ selectedScore }} out of 5
    </div>
    <div :class="[$style.info]">
      <h3>{{ title }}</h3>
      <p>{{ description }}</p>
    </div>
  </modal-wrapper>
</template>

<script setup lang="ts">
import {ref} from 'vue';
import ModalWrapper from './ModalWrapper.vue';

const illustrationThankYou = new URL(
  '../assets/images/illustration-thank-you.svg',
  import.meta.url
).href;
const props = defineProps<{
  title: string;
  selectedScore?: number;
  description: string;
}>();
</script>

<style lang="scss" module>
.wrapper {
  @apply sm:px-8 px-6 sm:py-11 py-8 text-center;
}

.image {
  @apply flex justify-center mx-auto sm:max-w-full max-w-[144px];
}

.result {
  @apply sm:mt-8 mt-6 inline-block sm:px-5 px-3 py-2 rounded-[22.5px] bg-dark-blue text-orange sm:text-md text-sm;
  @apply leading-none;
}

.info {
  @apply sm:mt-10 mt-8 space-y-2.5;
}
</style>
