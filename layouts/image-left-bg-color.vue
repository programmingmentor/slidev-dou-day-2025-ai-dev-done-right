<script setup lang="ts">
import { computed } from "vue";
import { handleBackground, resolveAssetUrl } from "./layoutHelper";

const props = defineProps({
  image: {
    type: String,
  },
  class: {
    type: String,
  },
  backgroundSize: {
    type: String,
    default: "cover",
  },
  bgColor: {
    type: String,
    default: "white", // Default background color
  },
});

const style = computed(() => {
  const bgStyle = handleBackground(props.image, false, props.backgroundSize);
  return {
    ...bgStyle,
    backgroundColor: props.bgColor, // Apply the custom background color
  };
});
</script>

<template>
  <div
    class="grid grid-cols-2 w-full h-full auto-rows-fr"
    :style="{
      backgroundImage: `url('${resolveAssetUrl('/dou-bg-dark-01.png')}')`,
      backgroundSize: 'cover',
      backgroundPosition: 'center',
      backgroundRepeat: 'no-repeat',
    }"
  >
    <div class="w-full h-full" :style="style" />
    <div class="slidev-layout default" :class="props.class">
      <slot />
    </div>
  </div>
</template>
