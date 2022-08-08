<script setup lang="ts">
import { NButton } from 'naive-ui';
import { ref } from 'vue';

import type { Elements, FlowExportObject } from '@braks/vue-flow';
import { VueFlow, useVueFlow } from '@braks/vue-flow';

const elements = ref<Elements>([
  { id: '1', type: 'input', label: 'Node 1', position: { x: 250, y: 5 } },
  { id: '2', type: 'input', label: 'Node 2', position: { x: 350, y: 50 } },
]);

const { onPaneReady, toObject } = useVueFlow({
  defaultZoom: 3,
  minZoom: 0.4,
  maxZoom: 4,
});

onPaneReady(({ fitView }) => {
  fitView();
});

const doSaveTemplate = () => {
  const flow: FlowExportObject = toObject();
  if (flow.nodes.length) {
    console.log(flow);
  }
};
</script>

<template>
  <div style="height: 800px">
    <div ref="boardContainer"
      style="height: 700px"
      class="dndflow">
      <VueFlow v-model="elements"
        class="basicflow"
        :default-edge-options="{ type: 'smoothstep' }">
      </VueFlow>

      <div style="position: absolute; right: 15px; top: 5px; z-index: 4"
        class="">
        <n-space>
          <div mt-1>
            <n-button type="success"
              @click="doSaveTemplate"> Save </n-button>
          </div>
        </n-space>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
