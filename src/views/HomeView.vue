<template>
  <div class="home">
    <border-block border-radius="50" border-width="12" class="btn-wrap">
      <template #content="{ maskImage }">
        <div class="btn-content" :style="{ maskImage }">Simple</div>
      </template>
      <template #border="{ maskImage }">
        <div class="btn-border" :style="{ maskImage }"></div>
      </template>
    </border-block>
    <border-block
      style="margin-left: 32px"
      border-radius="50"
      border-width="15"
      class="btn-wrap"
      stroke-dasharray="20,4"
      stroke-dashoffset="5"
    >
      <template #content="{ maskImage }">
        <div class="btn-content" :style="{ maskImage }">Dashed</div>
      </template>
      <template #border="{ maskImage }">
        <div class="btn-border" :style="{ maskImage }"></div>
      </template>
    </border-block>
    <border-block
      style="margin-left: 32px"
      border-radius="50"
      border-width="1"
      class="btn-wrap"
    >
      <template #content="{ maskImage }">
        <div class="btn-content" :style="{ maskImage }">-- Thin --</div>
      </template>
      <template #border="{ maskImage }">
        <div class="btn-border" :style="{ maskImage }"></div>
      </template>
    </border-block>
  </div>
</template>

<script lang="ts" setup>
import BorderBlock from "@/components/BorderBlock.vue";
</script>

<style>
.home {
  text-align: center;
  grid-gap: 16px;
  padding: 32px;
  height: 100vh;
  box-sizing: border-box;
  background: url("https://images.pexels.com/photos/370799/pexels-photo-370799.jpeg?cs=srgb&dl=pexels-dana-tentis-370799.jpg&fm=jpg");
  animation: bg-migration 12s ease-in-out infinite;
  background-size: 150%;
}
.btn-wrap {
  cursor: pointer;
}

.btn-content {
  display: flex;
  justify-content: center;
  transition: all 0.2s;
  background-color: rgba(128, 0, 83, 0.34);
  padding: 2rem 4rem;
  color: white;
  font-size: 4em;
}

.btn-wrap:hover .btn-content {
  background-color: rgba(0, 41, 128, 0.34);
}

.btn-border:after,
.btn-border:before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  transition: opacity 0.5s;
}

.btn-border:after {
  opacity: 0;
  background: linear-gradient(
    90deg,
    rgba(86, 81, 166, 1) 0%,
    rgba(9, 9, 121, 1) 35%,
    rgba(0, 212, 255, 1) 100%
  );
}
.btn-border:before {
  background: linear-gradient(
    90deg,
    rgb(128, 81, 166) 0%,
    rgb(121, 9, 89) 35%,
    rgb(255, 38, 0) 100%
  );
}

.btn-wrap:hover .btn-border:before {
  opacity: 0;
}
.btn-wrap:hover .btn-border:after {
  opacity: 1;
}

@keyframes bg-migration {
  0% {
    background-position-x: -20px;
    background-position-y: -10px;
  }
  33% {
    background-position-x: 0;
    background-position-y: 0;
  }
  67% {
    background-position-x: -10px;
    background-position-y: -15px;
  }
  100% {
    background-position-x: -20px;
    background-position-y: -10px;
  }
}
</style>
