<script setup>
import { onMounted, computed } from "vue";
import Toast from "primevue/toast";
import { useMediaQuery } from "@vueuse/core";

const toast = useToast();
const isMobile = useMediaQuery("(max-width: 768px)");
const toastPosition = computed(() =>
   isMobile.value ? "bottom-center" : "top-center",
);

onMounted(() => {
   toast.add({
      severity: "warn",
      summary: "BELANGRIJK NIEUWS",
      detail: "Het evenement is helaas geannuleerd",
      life: 0,
   });
});
</script>
<template>
   <div class="flex min-h-screen flex-col bg-gray-100">
      <ScrollTop
         :threshold="100"
         icon="pi pi-arrow-up"
         :pt="{
            root: 'w-2rem h-2rem border-round-sm bg-white',
            icon: {
               class: 'text-base text-black',
            },
         }"
      />
      <Toast
         :position="toastPosition"
         :pt="{ root: { style: 'opacity: 1' } }"
      />
      <main class="flex-1">
         <slot />
      </main>
      <footer>
         <Footer />
      </footer>
   </div>
</template>
