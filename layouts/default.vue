<template>
  <div>
    <the-header />
    <Nuxt keep-alive />
    <the-footer />
  </div>
</template>

<script>
import TheHeader from "@/components/TheHeader";
import TheFooter from "@/components/TheFooter";

export default {
  components: {
    TheHeader,
    TheFooter,
  },
};
</script>
