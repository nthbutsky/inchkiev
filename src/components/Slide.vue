<template>
  <div class="slide">
    <transition name="slide-fade">
      <slot />
    </transition>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss">
.slide-fade-enter-active {
  transition: all 0.5s ease;
}
.slide-fade-leave-active {
  transition: all 1s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter,
.slide-fade-leave-to {
  transform: translateX(-200px);
  opacity: 0;
}
</style>
