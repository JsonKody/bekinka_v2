<script setup lang="ts">
const props = defineProps<{
  isDesc: boolean
  fromBest: boolean
  sortByDate: boolean
}>()

const emit = defineEmits<{
  (e: 'update:isDesc', value: boolean): void
  (e: 'update:fromBest', value: boolean): void
  (e: 'update:sortByDate', value: boolean): void
}>()

const handleDateClick = () => {
  if (props.sortByDate) {
    emit('update:isDesc', !props.isDesc)
  } else {
    emit('update:sortByDate', true)
  }
}

const handleScoreClick = () => {
  if (props.sortByDate) {
    emit('update:sortByDate', false)
  } else {
    emit('update:fromBest', !props.fromBest)
  }
}
</script>

<template>
  <div>
    <!-- Date Sort -->
    <button
      @click="handleDateClick"
      class="select-none font-asap font-semibold text-lg cursor-pointer p-2 focus:outline-none trans-200"
      :class="{
        'text-pink-400 hover:text-pink-300': sortByDate,
        'text-purple-300/30 hover:text-purple-300/50': !sortByDate,
      }"
    >
      <template v-if="isDesc">
        Od nejnovějších
        <IconComponent name="ArrDown" size="1.5rem" />
      </template>
      <template v-else>
        Od nejstarších
        <IconComponent name="ArrUp" size="1.5rem" />
      </template>
    </button>

    <!-- Score Sort -->
    <button
      @click="handleScoreClick"
      class="select-none font-asap font-semibold text-lg cursor-pointer p-2 focus:outline-none trans-200"
      :class="{
        'text-purple-300/30 hover:text-purple-300/50': sortByDate,
        'text-pink-400 hover:text-pink-300': !sortByDate,
      }"
    >
      <template v-if="fromBest">
        Od nejlepších <IconComponent name="ArrDown" size="1.5rem" />
      </template>
      <template v-else> Od nejhorších <IconComponent name="ArrUp" size="1.5rem" /> </template>
    </button>
  </div>
</template>

