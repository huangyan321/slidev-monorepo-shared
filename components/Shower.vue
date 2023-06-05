<!-- @format -->

<script setup lang="ts">
import { ref } from 'vue';

const props = defineProps({
  count: {
    default: 0,
  },
});

const counter = ref(props.count);
</script>

<template>
  <div flex="~" w="min" border="~ main rounded-md">
    <div
      style="
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-flow: nowrap row;
        text-align: center;
      "
    >
      <div class="w-80% m-2" v-click>
        <img src="/vue3.png" alt="alt text" />
        <p>vue3</p>
      </div>
      <div class="w-50% m-2" v-click>
        <img src="/element-plus.png" alt="alt text" />
        <p>element-plus</p>
      </div>
      <div class="w-50% m-2" v-click>
        <img src="/vben.png" alt="alt text" />
        <p>vben-admin</p>
      </div>
    </div>
  </div>
</template>
