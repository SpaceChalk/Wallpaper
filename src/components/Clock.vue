<script setup>
import {ref, onMounted, onUnmounted, computed} from 'vue';

const now = ref(new Date());
let timer = null;

onMounted(() => {
  timer = setInterval(() => {
    now.value = new Date()
  }, 1000);
})

onUnmounted(() => {
  clearInterval(timer);
})

const hour = computed(() => {
  return now.value.getHours().toLocaleString('de-DE',
      {minimumIntegerDigits: 2, useGrouping: false});
})

const minute = computed(() => {
  return now.value.getMinutes().toLocaleString('en-US',
      {minimumIntegerDigits: 2, useGrouping: false});
})

const second = computed(() => {
  return now.value.getSeconds().toLocaleString('en-US',
      {minimumIntegerDigits: 2, useGrouping: false});
})

const period = computed(() => {
  return now.value.getHours() < 12 ? '"AM"' : '"PM"';
})

const day = computed(() => {
  return now.value.getDate().toLocaleString('en-US',
      {minimumIntegerDigits: 2, useGrouping: false});
})

const month = computed(() => {
  return now.value.toLocaleString('default', {month: 'long'});
})

const year = computed(() => {
  return now.value.getFullYear();
})
</script>

<template>
  <div class="main-container">
    <div class="block-tag">
      <span>clock.js</span>
      <div class="circle"></div>
    </div>

    <div class="block">
      <div class="block-content">
        <div class="left-content">
          <span class="variable-box">let</span>
          <div class="appendage-container">
            <span style="color: rgb(243, 224, 84); font-size: 24px; font-weight: 600">]</span>
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">;</span>
          </div>
        </div>

        <div class="content-box">
          <div class="start">
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">clock</span>
            <span
                style="color: rgb(68, 177, 249); font-size: 24px; font-weight: 600; padding-right: 10px; padding-left: 10px">=</span>
            <span style="color: rgb(243, 224, 84); font-size: 24px; font-weight: 600">[</span>
          </div>

          <div class="content-row">
            <span style="color: rgb(214,114,119); font-size: 24px; font-weight: 600">hour</span>
            <span style="color: rgb(68, 177, 249); font-size: 24px; font-weight: 600">:</span>
            <span style="color: rgb(203,156,107); font-size: 24px; font-weight: 600; margin-left: 10px">{{
                hour
              }}</span>
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">,</span>
          </div>

          <div class="content-row">
            <span style="color: rgb(214,114,119); font-size: 24px; font-weight: 600">minute</span>
            <span style="color: rgb(68, 177, 249); font-size: 24px; font-weight: 600">:</span>
            <span style="color: rgb(203,156,107); font-size: 24px; font-weight: 600; margin-left: 10px">{{
                minute
              }}</span>
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">,</span>
          </div>

          <div class="content-row">
            <span style="color: rgb(214,114,119); font-size: 24px; font-weight: 600">second</span>
            <span style="color: rgb(68, 177, 249); font-size: 24px; font-weight: 600">:</span>
            <span style="color: rgb(203,156,107); font-size: 24px; font-weight: 600; margin-left: 10px">{{
                second
              }}</span>
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">,</span>
          </div>

          <div class="content-row">
            <span style="color: rgb(214,114,119); font-size: 24px; font-weight: 600">period</span>
            <span style="color: rgb(68, 177, 249); font-size: 24px; font-weight: 600">:</span>
            <span style="color: rgb(103, 181, 103); font-size: 24px; font-weight: 600; margin-left: 10px">{{
                period
              }}</span>
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">,</span>
          </div>

          <div class="content-row">
            <span style="color: rgb(214,114,119); font-size: 24px; font-weight: 600">day</span>
            <span style="color: rgb(68, 177, 249); font-size: 24px; font-weight: 600">:</span>
            <span style="color: rgb(203,156,107); font-size: 24px; font-weight: 600; margin-left: 10px">{{ day }}</span>
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">,</span>
          </div>

          <div class="content-row">
            <span style="color: rgb(214,114,119); font-size: 24px; font-weight: 600">month</span>
            <span style="color: rgb(68, 177, 249); font-size: 24px; font-weight: 600">:</span>
            <span style="color: rgb(103, 181, 103); font-size: 24px; font-weight: 600; margin-left: 10px">"{{
                month
              }}"</span>
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">,</span>
          </div>

          <div class="content-row">
            <span style="color: rgb(214,114,119); font-size: 24px; font-weight: 600">year</span>
            <span style="color: rgb(68, 177, 249); font-size: 24px; font-weight: 600">:</span>
            <span style="color: rgb(203,156,107); font-size: 24px; font-weight: 600; margin-left: 10px">{{
                year
              }}</span>
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">,</span>
          </div>

        </div>
      </div>
    </div>

    <div class="block-tag" style="margin-top: 20px; width: 140px">
      <span>README.md</span>
      <div class="circle" style="margin: 0; background-color: #44B1F9FF"></div>
    </div>

    <div class="small-block">
      <div class="block-content" style="flex-direction: column">

        <div style="display: inline-flex">
          <span class="description" style="color: #CB9C6BFF">
            #
          </span>
          <span class="description" style="color: #C07CDAFF; font-style: italic">
           Instruction
          </span>
        </div>

        <div style="padding-left: 14px">
          <span class="description" style="padding-left: 0">
            1. Hide Desktop Icons manually or with Wallpaper Engine
          </span>
        </div>

        <div style="padding-left: 14px">
          <span class="description" style="padding-left: 0">
            2. Type task into the function and press enter to confirm
          </span>
        </div>

      </div>
    </div>
  </div>
</template>

<style scoped>
.main-container {
  flex-flow: row;
  justify-content: center;
  align-items: center;
  grid-auto-columns: 1fr;
  gap: 27px;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto auto;
  text-align: left;
}

.block-tag {
  position: relative;
  left: 30px;
  right: auto;
  z-index: auto;
  display: flex;
  width: 125px;
  height: 30px;
  padding-right: 12px;
  padding-left: 12px;
  justify-content: space-between;
  align-items: center;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  background-color: rgb(81, 87, 98);
}

.circle {
  width: 13px;
  height: 13px;
  border-radius: 100px;
  background-color: rgb(246, 114, 114);
}

.block {
  width: 340px;
  height: 400px;
  border-style: solid;
  border-width: 8px;
  border-color: rgb(81, 87, 98);
  border-radius: 30px;
  align-content: center;
}

.block-content {
  display: flex;
  height: 90%;
  justify-content: center;
  align-items: flex-start;
  gap: 12px;
  font-size: 14px;
}

.left-content {
  display: flex;
  height: 100%;
  margin-right: 0px;
  margin-left: 0px;
  flex-flow: column;
  justify-content: space-between;
  align-items: flex-start;
  grid-auto-columns: 1fr;
  gap: 0px;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto auto;
}

.small-block {
  width: 340px;
  min-height: 200px;
  max-height: 300px;
  height: 100%;
  border-style: solid;
  border-width: 8px;
  border-color: rgb(81, 87, 98);
  border-radius: 25px;
  align-content: center;
  display: flex;
  padding-top: 20px;
  padding-bottom: 20px;
  text-wrap: normal;
}

.description {
  padding-left: 14px;
  font-size: 13px;
  font-weight: 500;
}

.variable-box {
  display: block;
  margin-left: auto;
  order: 0;
  flex: 1 1 0%;
  color: rgb(192, 124, 218);
  font-size: 24px;
  font-weight: 600;
}

.appendage-container {
  flex-flow: row;
  flex: 0 1 auto;
}

.content-box {
  overflow: visible;
  box-sizing: border-box;
  flex-flow: column;
  justify-content: center;
  align-items: flex-start;
  flex: 0 1 auto;
  gap: 12px;
  object-fit: contain;
  object-position: 0% 50%;
}

.start {
  display: flex;
  margin-right: 0;
  margin-left: 0;
  align-self: auto;
  gap: 0;
}

.content-row {
  display: flex;
  margin-right: 0px;
  margin-left: 0px;
  justify-content: flex-start;
  align-items: stretch;
  align-self: auto;
  flex: 0 1 auto;
}
</style>