<script setup lang="ts">
import { type Ref, ref, watch } from 'vue'
import { onClickOutside, useElementVisibility } from '@vueuse/core'

interface Props {
  label: string
  top?: boolean
  bottom?: boolean
  width?: string
  theme?: 'dark' | 'light'
}

const props = defineProps<Props>()

const opened = ref<boolean>(false)

const root: Ref<HTMLElement | null> = ref(null)

const visible = useElementVisibility(root)

onClickOutside(root, () => (opened.value = false))

const transitionName = () => {
  if (props.bottom) {
    return 'slide-down'
  } else {
    return 'slide-up'
  }
}

watch(
  visible,
  (newValue, oldValue) => {
    if (!newValue && oldValue) opened.value = false
  },
  {
    immediate: true
  }
)
</script>
<template>
  <div
    ref="root"
    class="dropper-root"
    :class="{
      opened: opened,
      top: top,
      bottom: bottom,
      'dark-theme': theme == 'dark',
      'light-theme': theme == 'light'
    }"
    :style="{
      width: width
    }"
    @click="opened = !opened"
  >
    <span>{{ label }}</span>
    <svg xmlns="http://www.w3.org/2000/svg" width="1.2em" height="1.2em" viewBox="0 0 24 24">
      <path
        fill="none"
        stroke="currentColor"
        strokeLinecap="round"
        strokeLinejoin="round"
        strokeWidth="2"
        d="m6 9l6 6l6-6"
      ></path>
    </svg>
    <transition :name="transitionName()">
      <div v-if="opened" class="list-group">
        <slot />
      </div>
    </transition>
  </div>
</template>
<style lang="scss">
@import '../assets/styles/_mixins';
@import '../assets/styles/_variables';
@import '../assets/styles/_vue_transitions';

.dropper-root {
  @include animate(0.3s, all);
  @include user-select-none;

  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;

  gap: 10px;

  position: relative;
  cursor: pointer;

  padding: 0px 10px 0px 15px;
  border-radius: 10px;
  height: 40px;

  min-width: fit-content;

  z-index: 2;

  background: var(--border-color);
  border: 1px solid var(--border-color);

  > span {
    @include text-style-main;

    color: var(--fill-color);
  }

  > svg {
    path {
      stroke-width: 1.5;
      stroke: var(--fill-color);
    }
  }

  > .list-group {
    @include bg-blur;
    @include hide-scrollbar;

    display: flex;
    flex-direction: column;

    position: absolute;

    overflow-x: hidden;
    overflow-y: scroll;

    left: 0px;
    right: 0px;
    border-radius: 10px;

    background: var(--border-color);
    border: 1px solid var(--border-color);

    z-index: 1;

    max-height: 200px;

    > * {
      padding: 10px 10px 10px 15px;
      height: fit-content;

      text-align: left;

      border-top: 1px solid var(--border-color);
      color: var(--fill-color);

      @include text-style-main;

      &:hover {
        background: var(--border-color);
      }
    }
  }

  &.opened {
    svg {
      rotate: 180deg;
    }
  }

  // Apperance

  &.dark-theme {
    --fill-color: #{$color-dark-theme-fill};
    --border-color: #{$color-dark-theme-border};
  }

  &.light-theme {
    --fill-color: #{$color-light-theme-fill};
    --border-color: #{$color-light-theme-border};
  }

  &.top {
    > .list-group {
      bottom: 45px;

      > * {
        &:first-of-type {
          border-top: transparent;
        }
      }
    }

    svg {
      transform: scaleY(-1);
    }
  }

  &.bottom {
    > .list-group {
      top: 45px;

      > * {
        &:first-of-type {
          border-top: transparent;
        }
      }
    }
  }
}
</style>
