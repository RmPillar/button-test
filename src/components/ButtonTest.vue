<template>
  <div
    class="rounded-full overflow-hidden border border-red-500 w-[150px] h-[150px] relative flex items-center justify-center"
    ref="buttonRef"
  >
    <span class="relative z-10">Test</span>
    <div
      class="absolute w-[150px] h-[150px] top-0 left-0 transition-opacity duration-300"
      ref="bgRef"
    >
      <div
        class="absolute rounded-full w-full h-full top-0 right-0 -translate-x-1/2 -translate-y-1/2 bg-red-500"
      />
    </div>
  </div>
</template>

<script setup>
  import { ref, onMounted } from "vue";

  const buttonRef = ref(null);
  const bgRef = ref(null);

  onMounted(() => {
    const { top, left } = buttonRef.value.getBoundingClientRect();
    window.addEventListener("mousemove", ({ x, y }) => {
      const distanceFromCentre = Math.sqrt(
        Math.pow(x - left - 75, 2) + Math.pow(y - top - 75, 2)
      );

      if (distanceFromCentre < 200) {
        bgRef.value.classList.remove("opacity-0");

        bgRef.value.style.transform = `translate(${x - left}px,${y - top}px)`;
      }
      if (distanceFromCentre > 200) {
        bgRef.value.classList.add("opacity-0");
      }
    });
  });
</script>
