<template lang="pug">
section.sidebar-group
  a.sidebar-heading.clickable(
    v-if="item.link",
    :class="{ active: isActive(route, item.link) }",
    :href="item.link"
  )
    span {{ item.text }}

  p.sidebar-heading(
    v-else,
    :class="{ active: isActive(route, item.link) }"
  )
    span {{ item.text }}

  SidebarLinks.sidebar-group-items(:items="item.items")
</template>

<script setup lang="ts">
import { useRoute, type Route } from 'vitepress';
import { isActive } from '../helpers';
import SidebarLinks from './SidebarLinks.vue';
import type { TSidebarItem } from '../types';

type Props = {
  item: TSidebarItem;
};

defineProps<Props>();

const route: Route = useRoute();
</script>

<style lang="scss">
.sidebar-heading {
  color: var(--text-color);
  font-weight: bold;
  line-height: 2;
  cursor: pointer;
  margin: 0;

  &.router-link-exact-active,
  &.active {
    color: var(--accent-color);
  }

  &:hover {
    color: var(--accent-color);
  }
}
</style>
