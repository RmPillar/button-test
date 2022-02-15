<template>
  <div
    class="rounded-full w-[148px] h-[148px] relative mix-blend-difference"
    ref="buttonRef"
  >
    <div
      class="absolute rounded-full w-full h-full top-0 right-0 -translate-x-1/2 -translate-y-1/2 bg-black border-2 border-black"
    />
  </div>
</template>

<script setup>
  import { ref, onMounted } from "vue";

  const buttonRef = ref(null);

  onMounted(() => {
    const { top, left } = buttonRef.value.getBoundingClientRect();
    window.addEventListener("mousemove", ({ x, y }) => {
      buttonRef.value.style.transform = `translate(${x - left}px,${y - top}px)`;
    });
  });
</script>
