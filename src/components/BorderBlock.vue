<template>
  <div
    class="wrap"
    :style="{
      padding: `${borderWidth}px !important`,
    }"
  >
    <slot name="content" :maskImage="maskContent" />
    <slot name="border" :maskImage="mask" />
  </div>
</template>

<script lang="ts" setup>
import { computed, defineProps } from "vue";

const props = defineProps<{
  borderWidth: number;
  borderRadius: number;
  strokeDasharray?: string;
  strokeDashoffset?: number;
}>();

const getMask = (w: number, r: number, isContent = false) =>
  [
    `url("data:image/svg+xml,%3Csvg`,
    `xmlns='http://www.w3.org/2000/svg'`,
    `width='100%'`,
    `height='100%'%3E%3Crect`,
    !isContent && `fill='transparent'`,
    `stroke='black'`,
    `stroke-width='${w}'`,
    `stroke-dasharray='${(!isContent && props.strokeDasharray) || ""}'`,
    `stroke-dashoffset='${(!isContent && props.strokeDashoffset) || 0}'`,
    `style='rx: ${
      !isContent ? `${r}px` : `${Math.max(0, r - w)}px`
    }; width: calc(100% - ${w}px); height: calc(100% - ${w}px);'`,
    `x='${w / 2}'`,
    `y='${w / 2}'`,
    `width='100%'`,
    `height='100%'/%3E%3C/svg%3E")`,
  ]
    .filter((e) => e)
    .join(" ");

const mask = computed(() => getMask(props.borderWidth, props.borderRadius));
const maskContent = computed(() =>
  getMask(props.borderWidth, props.borderRadius, true)
);
</script>

<style scoped>
.wrap {
  position: relative !important;
  display: inline-block !important;
  box-sizing: border-box !important;
  background-color: transparent !important;
  mask-repeat: no-repeat !important;
  mask-position: center !important;
  min-width: min-content;
}

.wrap :slotted(*):first-child {
  position: relative !important;
}

.wrap :slotted(*):last-child {
  position: absolute !important;
  left: 0 !important;
  top: 0 !important;
  right: 0 !important;
  bottom: 0 !important;
  mask-repeat: no-repeat !important;
  mask-position: center !important;
  pointer-events: none !important;
}
</style>
