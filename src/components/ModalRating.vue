<template>
  <modal-wrapper :class="[$style.wrapper]">
    <div :class="[$style.top]">
      <div :class="[$style.icon]">
        <IconStar />
      </div>
    </div>
    <div :class="[$style.info]">
      <h3>{{ title }}</h3>
      <p>{{ description }}</p>
    </div>
    <ul :class="[$style.scores]">
      <li
        :class="[
          [$style.score],
          {
            [$style['score--active']]: score === selectedScore,
          },
        ]"
        v-for="score in scores"
        :key="score"
      >
        <button @click="handleSelectScore(score)">
          {{ score }}
        </button>
      </li>
    </ul>
    <app-button class="w-full sm:mt-8 mt-6" @click="handleSubmitScore"
      >Submit</app-button
    >
  </modal-wrapper>
</template>

<script setup lang="ts">
import {ref} from 'vue';
import AppButton from '@components/AppButton.vue';
import IconStar from '@icons/icon-star.svg';
import ModalWrapper from '@components/ModalWrapper.vue';

const props = defineProps<{
  title: string;
  description: string;
  onSubmitScore?: (score: number) => void;
}>();

const scores = ref([1, 2, 3, 4, 5]);
const selectedScore = ref<number>();

function handleSelectScore(score: number) {
  selectedScore.value = score;
}

function handleSubmitScore() {
  if (typeof selectedScore.value === 'number') {
    props.onSubmitScore?.(selectedScore.value);
  }
}
</script>

<style lang="scss" module>
.wrapper {
  @apply sm:pl-8 pl-6 sm:pt-8 pt-6 pb-8 sm:pr-10 pr-6;
}

.score button,
.icon {
  @apply flex justify-center items-center rounded-full text-medium-grey bg-dark-blue font-bold;
}

.icon {
  @apply sm:mb-9 mb-5 sm:w-[48px] sm:h-[48px] w-10 h-10 text-orange;
}

.info {
  @apply space-y-2.5;
}

.scores {
  @apply flex flex-wrap justify-evenly sm:gap-5 gap-4 sm:mt-5 mt-6;
}

.score {
  button {
    @apply sm:text-base sm:w-[51px] sm:h-[51px] w-[42px] h-[42px] text-sm leading-none;

    &:hover {
      @apply bg-medium-grey text-pure-white;
    }
  }

  &--active button,
  &--active button:hover {
    @apply bg-orange text-pure-white;
  }
}
</style>
