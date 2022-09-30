<template>
      <v-text-field
      v-model.lazy="value"
      @change="submitInput()"
      class="text-field"
      placeholder="Enter text"
      :readonly="disabled"
      dense
      outlined
    ></v-text-field>
</template>

<script>
export default {
  props: {
    disabled: {
      type: Boolean,
      reqired: true
    },
    propValue: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      value: ""
    };
  },
  methods : {
    submitInput() {
      this.$emit("input", this.value);
    }
  },
  mounted() {
    this.value = this.propValue
  },
  watch: {
    value(newValue) {
      this.value = newValue
    }
  }
};
</script>

<style scoped></style>
