<template>
  <div :class="[$style.wrapper]">
    <modal-rating
      v-if="!isSubmitScore"
      title="How did we do?"
      description="Please let us know how we did with your support request. All feedback is appreciated to help us improve our offering!"
      @submit-score="handleSubmitScore"
    />
    <modal-rating-success
      v-else
      title="Thank you!"
      :selected-score="selectedScore"
      description="We appreciate you taking the time to give a rating. If you ever need more support, don’t hesitate to get in touch!"
    />
  </div>
</template>

<script setup lang="ts">
import {ref} from 'vue';
import ModalRating from '@components/ModalRating.vue';
import ModalRatingSuccess from '@components/ModalRatingSuccess.vue';

const selectedScore = ref<number | undefined>();
const isSubmitScore = ref(false);

function handleSubmitScore(score: number) {
  selectedScore.value = score;
  isSubmitScore.value = true;
}
</script>

<style lang="scss" module>
.wrapper {
  @apply p-8 min-h-screen flex justify-center items-center;
}
</style>
