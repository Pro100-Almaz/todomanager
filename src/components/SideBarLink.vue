<template>
    <router-link :to = "to" class = "link" :class="{active: isActive}">
        <i class="icon" :class="icon" style="font-size: 1.2rem"/>
        <transition name="fade">
            <span v-if="isExpanded" class="link__text">
                <slot/>
            </span>
        </transition>
    </router-link>
</template>

<script setup lang="ts">
import { defineProps, computed, ref } from "vue";
import { useRoute } from "vue-router";
import {useSidebarStore} from './state';
const props = defineProps({
    to: {
      type: String,
      required: true
    },
    icon: {
        type: String,
        required: true
    }
})
const store = useSidebarStore();
const isExpanded = computed(() => store.is_expanded);
const route = useRoute();
const isActive = computed(() => route.path === props.to);
</script>

<style scoped>
.link {
  display: flex;
  flex-direction: row;
  align-items: center;
  cursor: pointer;
  position: relative;
  font-weight: 400;
  font-size: 16px;
  margin: 0.1em 0;
  padding: 0.4em;
  border-radius: 0.25em;
  height: 1.5em;
  color: white;
  text-decoration: none;
}
.link__text{
  white-space: nowrap;
}
.link:hover {
  background-color: var(--sidebar-item-hover);
}
.link.active {
  background-color: var(--sidebar-item-active);
}
.link .icon {
  flex-shrink: 0;
  width: 25px;
  margin-right: 10px;
}
</style>