<template>
  <div class="h-full flex flex-col slidev-layout default">
    <slot />
    <div class="flex-grow"></div>
    <slot name="bottom"></slot>
  </div>
</template>