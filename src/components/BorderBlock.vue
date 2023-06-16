<template>
  <div
    class="wrap"
    :style="{
      maskImage: maskWrap,
      padding: `${borderWidth}px`,
    }"
  >
    abcdfsdfsdf
    <div
      class="border"
      ref="border"
      :style="{
        maskImage: mask,
      }"
    ></div>
  </div>
</template>

<script lang="ts" setup>
import { computed, ref } from "vue";

const borderWidth = 100;
const borderRadius = `100px`;

const getMask = (w: number, r: string, isWrap = false) =>
  [
    `url("data:image/svg+xml,%3Csvg`,
    `xmlns='http://www.w3.org/2000/svg'`,
    `width='100%'`,
    `height='100%'%3E%3Crect`,
    `fill='${!isWrap ? "transparent" : "black"}'`,
    `stroke='black'`,
    `stroke-width='${w}'`,
    `style='rx: ${r}; width: calc(100% - ${w}px); height: calc(100% - ${w}px);'`,
    `x='${w / 2}'`,
    `y='${w / 2}'`,
    `width='100%'`,
    `height='100%'/%3E%3C/svg%3E")`,
  ].join(" ");

const mask = computed(() => getMask(borderWidth, borderRadius));
const maskWrap = computed(() => getMask(borderWidth, borderRadius, true));

const border = ref<HTMLDivElement>();
</script>

<style>
.wrap {
  position: relative !important;
  display: inline-block !important;
  box-sizing: border-box !important;
  background-color: red !important;
  z-index: 1 !important;
  mask-repeat: no-repeat !important;
  mask-position: center !important;
}
.border {
  z-index: -1 !important;
  position: absolute !important;
  transition: all 0.5s !important;
  background: linear-gradient(
    90deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(9, 9, 121, 1) 35%,
    rgba(0, 212, 255, 1) 100%
  ) !important;
  opacity: 0.4 !important;
  left: 0 !important;
  top: 0 !important;
  right: 0 !important;
  bottom: 0 !important;
  mask-repeat: no-repeat !important;
  mask-position: center !important;
}
</style>
