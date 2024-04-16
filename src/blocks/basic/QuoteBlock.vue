<script setup lang="ts">
import { Error, Success, Wallet } from '@icon-park/vue-next'
import { onMounted, onUnmounted, ref} from 'vue';
import type { QuoteBlockInfo } from '@/types/block'


const STATUS_MAP = {
  success: {
    color: '#059669',
    bgColor: '#E4F2E9',
    borderColor: '#79DBA2',
    icon: Success
  },
  warning: {
    color: '#E18F05',
    bgColor: '#F8ECEC',
    borderColor: '#79DBA2',
    icon: Error
  },
  error: {
    color: '#DC2C26',
    bgColor: '#F8ECEC',
    borderColor: '#F3A9A5',
    icon: Wallet
  }
}

const props = defineProps<{
  blockInfo: QuoteBlockInfo
}>()
// console.log(props.blockInfo);
// onMounted(() => {
//   console.log(props.blockInfo, 'x,,x');
//   props.blockInfo.lifecycle.mounted()
// })
// onUnmounted(() => {
//   console.log(3);
// })
const { color, bgColor, /* borderColor, */ icon } = STATUS_MAP[props.blockInfo.props.status]
  // 拿到当前组件的实例
  // const quoteRef = ref<HTMLDivElement | null>(null)
function click() {
  props.blockInfo.actions.onClick(props.blockInfo);
  console.log(props.blockInfo);
  
}
</script>

<template>
  <div
    @click="click"
    class="quote"
    ref="quoteRef"
    :style="{ backgroundColor: bgColor, color /* , border: `1px solid ${borderColor}` */ }"
  >
    <component :is="icon" />
    <span class="quote-text">{{ props.blockInfo.props.content }}</span>
  </div>
</template>

<style scoped>
.quote {
  display: flex;
  align-items: center;
  flex: 1;
  font-size: var(--font-size-large);
  padding: 8px 18px;
  border-radius: 8px;

  /* background-color: ; */
}

.quote-text {
  margin-left: 6px;
}
</style>
