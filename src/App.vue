<template>
  <div class="w-full h-96 bg-slate-800">
    <div class="w-80">
      <ColorPicker v-model:color="color" />
    </div>
  </div>
</template>

<script>
import ColorPicker from "./components/ColorPicker.vue";
export default {
  name: "App",
  data() {
    return {
      color: "",
    };
  },
  components: {
    ColorPicker,
  },
};
</script>

