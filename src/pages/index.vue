<script lang="ts" setup>
import { Icon } from '@iconify/vue';
import {
  useDashboard,
  LoadingStatus,
  type ChainConfig,
} from '@/stores/useDashboard';
import ChainSummary from '@/components/ChainSummary.vue';
import { computed, ref } from 'vue';
import { useBlockchain } from '@/stores';

const dashboard = useDashboard();

const keywords = ref('');
const chains = computed(() => {
  if (keywords.value) {
    return Object.values(dashboard.chains).filter(
      (x: ChainConfig) => x.chainName.indexOf(keywords.value) > -1
    );
  } else {
    return Object.values(dashboard.chains);
  }
});
const chainStore = useBlockchain()
</script>
<template>
  <div class="">
    <div class="flex md:!flex-row flex-col items-center justify-center mb-6 mt-14 gap-2">
      <div class="w-16 rounded-full">
        <svg version="1.0" xmlns="http://www.w3.org/2000/svg" 
          viewBox="0 0 250.000000 250.000000"
          preserveAspectRatio="xMidYMid meet">
          <g transform="translate(0.000000,250.000000) scale(0.100000,-0.100000)"
          :fill="chainStore.current?.themeColor||'#046909'" class=" dark:bold" stroke="none">
            <path d="M1069 2470 c-480 -75 -871 -416 -1003 -873 -37 -127 -46 -195 -46
            -343 0 -278 75 -511 238 -737 55 -77 202 -227 222 -227 6 0 10 63 10 172 l0
            172 -41 58 c-22 32 -60 100 -84 150 -219 467 -42 1004 418 1267 92 52 254 101
            374 111 117 10 177 7 296 -17 l77 -16 2 -51 c1 -57 4 -261 7 -468 l1 -138 155
            0 155 0 0 399 0 400 -67 31 c-187 89 -287 112 -498 116 -88 1 -185 -1 -216 -6z"/>
            <path d="M2000 2047 l0 -173 41 -54 c22 -30 60 -95 84 -145 180 -371 112 -802
            -174 -1098 -147 -153 -312 -243 -526 -288 -87 -19 -294 -14 -385 8 l-75 18 -3
            333 -2 332 -155 0 -155 0 0 -406 0 -405 72 -33 c178 -81 333 -116 514 -116
            217 0 370 35 561 131 141 70 229 133 331 237 238 243 362 562 349 902 -10 254
            -78 461 -219 668 -51 75 -229 262 -248 262 -6 0 -10 -67 -10 -173z"/>
            <path d="M650 1515 l0 -415 443 -2 442 -3 0 -263 0 -262 158 0 157 0 0 420 0
            420 -442 2 -443 3 -3 258 -2 257 -155 0 -155 0 0 -415z"/>
          </g>
        </svg>
      </div>
      <h1 class="text-primary dark:text-[#046909] text-3xl md:!text-6xl font-bold">
        {{ $t('pages.title') }}
      </h1>
      <div class="badge badge-primary badge-outline dark:text-[#046909] mt-1 text-sm md:!mt-8">
        {{ $t('pages.tag') }}
      </div>
    </div>
    <div class="text-center text-base">
      <p class="mb-1">
        {{ $t('pages.slogan') }}
      </p>
      <h2 class="mb-6">{{ $t('pages.description') }}</h2>
    </div>
    <div
      v-if="dashboard.status !== LoadingStatus.Loaded"
      class="flex justify-center"
    >
      <progress class="progress progress-info w-80 h-1"></progress>
    </div>

    <div class="flex items-center rounded-lg bg-base-100  border border-gray-200 dark:border-gray-700 mt-10">
      <Icon icon="mdi:magnify" class="text-2xl text-gray-400 ml-3"/>
      <input :placeholder="$t('pages.search_placeholder')" class="px-4 h-10 bg-transparent flex-1 outline-none text-base" v-model="keywords" />
      <div class="px-4 text-base hidden md:!block">{{ chains.length }}/{{ dashboard.length }}</div>
    </div>

    <div
      class="grid grid-cols-1 gap-4 mt-6 md:!grid-cols-3 lg:!grid-cols-4 2xl:!grid-cols-5"
    >
      <ChainSummary
        v-for="(chain, index) in chains"
        :key="index"
        :name="chain.chainName"
      />
    </div>
  </div>
</template>

<style scoped>
 .logo path{
  fill: #171d30;
}
</style>