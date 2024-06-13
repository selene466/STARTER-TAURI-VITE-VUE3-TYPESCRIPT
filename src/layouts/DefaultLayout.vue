<script setup lang="ts">
import { onMounted } from "vue";

// mounted
onMounted(() => {
  var width = 100;
  var height = 100;
  var elem = document.querySelector("#layout") as HTMLDivElement;
  if (elem) {
    elem.style.width = width + "vw";
    elem.style.height = height + "vh";
  }
  window.addEventListener("resize", () => {
    if (elem) {
      // auto width
      elem.style.width = width + "vw";
      if (width > 100) {
        width = 100;
      } else {
        width += 0.01;
      }

      // auto height
      elem.style.height = height + "vh";
      if (height > 100) {
        height = 100;
      } else {
        height += 0.01;
      }
    }
  });
});
</script>
<template>
  <div
    id="layout"
    class="h-full min-h-full bg-base-200 py-5 font-sans text-base"
  >
    <slot />
  </div>
</template>
