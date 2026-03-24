<script setup>
import {computed, ref} from "vue";

const hoveredId = ref(null);
const upHere = ref(false);
const newTaskText = ref("");
const tasks = ref([]);

const spaces = computed(() => {
  const minHeight = 34;
  const interval = 10;

  if(tasks.value.length < 2) {
    return minHeight + "%";
  }
  const calculatedHeight = (tasks.value.length * interval) + 25;

  return calculatedHeight < 500 ? `${calculatedHeight}%` : '500px';
})

const hovered = computed(() => {
  return upHere.value ? 1 : 0;
})
const removeCursor = (el) => {
  el.style.borderRightColor = 'transparent';
};

const removeTask = (taskId) => {
  tasks.value = tasks.value.filter(task => task.id !== taskId);
}

const addTask = () => {
  if (newTaskText.value.trim() === "") return;

  tasks.value.push({
    id: Date.now(),
    text: newTaskText.value
  });

  newTaskText.value = "";
};

</script>

<template>
  <div class="main-container">

    <div class="block-tag">
      <span>tasks.js</span>
      <div class="circle"></div>
    </div>

    <div class="block">
      <div class="block-content">

        <div class="left-content" :style="{ height: spaces }">
          <span class="variable-box">let</span>
          <div class="appendage-container">
            <span style="color: rgb(243, 224, 84); font-size: 24px; font-weight: 600">}</span>
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">;</span>
          </div>
        </div>

        <div class="content-box">

          <div class="start">
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">todo</span>
            <span
                style="color: rgb(68, 177, 249); font-size: 24px; font-weight: 600; padding-right: 10px; padding-left: 10px">=</span>
            <span style="color: rgb(243, 224, 84); font-size: 24px; font-weight: 600">{</span>
          </div>

          <transition-group name="typeout" tag="div" v-if="tasks.length" appear>
            <div
                v-for="(task, index) in tasks"
                :key="task.id"
                class="content-row"
                @mouseenter="hoveredId = task.id"
                @mouseleave="hoveredId = null"
            >
             <span style="color: rgb(214,114,119); font-size: 24px; font-weight: 600">task_{{ index + 1 }}</span>
             <span style="color: rgb(68, 177, 249); font-size: 24px; font-weight: 600">:</span>
             <span style="color: rgb(103,181,103); font-size: 24px; font-weight: 600; margin-left: 10px">"{{ task.text }}"</span>
             <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600; align-content: end">,</span>

              <div class="circle-container" :style="{ opacity: hoveredId === task.id ? 1 : 0 }">
               <div class="clear-circle" @click="removeTask(task.id)"></div>
             </div>
            </div>
          </transition-group>

          <div class="content-row" v-else>
            <span style="color: rgb(214,114,119); font-size: 24px; font-weight: 600">task</span>
            <span style="color: rgb(68, 177, 249); font-size: 24px; font-weight: 600">:</span>
            <span style="color: rgb(103,181,103); font-size: 24px; font-weight: 600; margin-left: 10px">"none"</span>
          </div>
        </div>
      </div>
    </div>

    <div class="block-tag" style="margin-top: 20px">
      <span>newTask.js</span>
      <div class="circle"></div>
    </div>

    <div class="small-block">
      <div class="block-content">
        <div class="left-content" style="min-height: 130px">
          <span class="variable-box" style="margin-right: 5px">const</span>
          <div class="appendage-container">
            <span style="color: rgb(243, 224, 84); font-size: 24px; font-weight: 600">}</span>
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">;</span>
          </div>
        </div>

        <div class="content-box">
          <div class="start">
            <span style="color: rgb(170, 179, 185); font-size: 24px; font-weight: 600">newToDo</span>
            <span
                style="color: rgb(68, 177, 249); font-size: 24px; font-weight: 600; padding-right: 10px; padding-left: 10px">=</span>
            <span style="color: rgb(243, 224, 84); font-size: 24px; font-weight: 600">{</span>
          </div>

          <div class="content-row">
            <span style="color: rgb(170,179,185); font-size: 24px; font-weight: 600">todo.</span>
            <span style="color: rgb(203,156,107); font-size: 24px; font-weight: 600">add</span>
            <span style="color: rgb(68,177,249); font-size: 24px; font-weight: 600">(</span>
            <div class="input-wrapper">

              <input
                  v-model="newTaskText"
                  @keyup.enter="addTask"
                  class="stealth-input"
                  :style="{ width: newTaskText.length > 0 ? newTaskText.length + 'ch' : '1px' }"
                  placeholder=""
              />
              <span class="custom-cursor"></span>

              <span v-if="!newTaskText" class="fake-placeholder">...</span>
            </div>
            <span style="color: rgb(68,177,249); font-size: 24px; font-weight: 600">)</span>
          </div>
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

.clear-circle {
  width: 24px;
  height: 24px;
  border-radius: 100px;
  background-color: rgb(246, 114, 114);
}

.circle-container {
  margin: 5px 5px 5px 25px;
  display: flex;
  align-content: center;
  opacity: 0;
  flex: 1;
}

.circle-container:hover {
  opacity: 1;
}

.small-block {
  min-width: 450px;
  max-width: 600px;
  min-height: 200px;
  max-height: 300px;
  height: 100%;
  border-style: solid;
  border-width: 10px;
  border-color: rgb(81, 87, 98);
  border-radius: 30px;
  align-content: center;
  display: flex;
  padding-top: 20px;
  padding-bottom: 20px;
  text-wrap: normal;
}

.block {
  min-width: 450px;
  max-width: 600px;
  min-height: 400px;
  max-height: 600px;
  height: 100%;
  border-style: solid;
  border-width: 10px;
  border-color: rgb(81, 87, 98);
  border-radius: 30px;
  align-content: center;
  display: flex;
  padding-top: 20px;
  padding-bottom: 20px;
}

.block-content {
  display: flex;
  min-height: 90%;
  align-items: flex-start;
  gap: 12px;
  font-size: 14px;
  padding-left: 32px;
}

.left-content {
  display: flex;
  flex-flow: column;
  justify-content: space-between;
  align-items: flex-start;
  flex: 1;
  transition-delay: 1.4s;
}

.variable-box {
  display: block;
  margin-left: auto;
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
  align-items: center;
  overflow: hidden;
  white-space: nowrap;
  width: 100%;
  border-right: 2px solid transparent;
}

.typeout-enter-active {
  animation: typing 2s steps(30, end) forwards;
  border-right: 2px solid orange;
}

.typeout-leave-active {
  pointer-events: none;
  width: 100%;
  animation: typing 1.5s steps(30, end) reverse forwards;
  border-right: 2px solid orange;
}

.typeout-move {
  transition: transform 0.5s ease;
}

@keyframes typing {
  from { width: 0; }
  to { width: 100%; }
}

.input-wrapper {
  display: inline-flex;
  align-items: center;
}

.stealth-input {
  background: transparent;
  border: none;
  outline: none;
  padding: 0;
  margin: 0;
  color: rgb(103,181,103);
  font-family: inherit;
  font-size: 24px;
  font-weight: 600;
  min-width: 10px;
  width: auto;
  caret-color: transparent;
  text-align: left;
}

.custom-cursor {
  width: 4px;
  height: 24px;
  background-color: orange;
  opacity: 0;
}

.fake-placeholder {
  position: relative;
  right: 4px;
  color: rgba(103,181,103, 0.3);
  pointer-events: none;
  font-size: 24px;
  font-weight: 600;
}

.input-wrapper:has(.stealth-input:focus) .custom-cursor {
  opacity: 1;
  animation: blink 1s step-end infinite;
}

@keyframes blink {
  from, to { opacity: 1; }
  50% { opacity: 0; }
}

.stealth-input:focus + .custom-cursor {
  display: inline-block;
}

.stealth-input:not(:focus) + .custom-cursor {
  display: none;
}

</style>