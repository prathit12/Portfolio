<template>
    <div>
        <Transition :name="name" :appear="appear">
            <div v-if="isVisible" :style="{ animationDuration: '${Duration}s', transitionDuration : '${duration}s'}">
                <slot>

                </slot>
            </div>

        </Transition>
    </div>

</template>

<script>

import { ref, onMounted, onBeforeUnmount } from 'vue';

export default {
  props: {
    name: String,
    appear: { type: Boolean, default: false },
    offsetTop: { type: Number, default: 0 },
    duration: { type: Number, default: 1 },
  },

  setup(props) {
    const isVisible = ref(false);
    const elementRef = ref(null);

    const inViewport = () => {
      const rect = elementRef.value.getBoundingClientRect();
      return rect.top <= (window.innerHeight - props.offsetTop) && rect.left <= window.innerWidth;
    };

    const detectVisibility = () => {
      isVisible.value = inViewport();
    };

    const debouncedDetectVisibility = debounce(detectVisibility, 100);

    onMounted(() => {
      detectVisibility();
      window.addEventListener('scroll', debouncedDetectVisibility, { passive: true });
      window.addEventListener('resize', debouncedDetectVisibility);
      window.addEventListener('orientationchange', debouncedDetectVisibility);
    });

    onBeforeUnmount(() => {
      window.removeEventListener('scroll', debouncedDetectVisibility);
      window.removeEventListener('resize', debouncedDetectVisibility);
      window.removeEventListener('orientationchange', debouncedDetectVisibility);
    });

    return {
      isVisible,
      elementRef,
    };
  },
};

function debounce(func, wait) {
  let timeout;
  return function () {
    const context = this;
    const args = arguments;
    const later = function () {
      timeout = null;
      func.apply(context, args);
    };
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
}
</script>