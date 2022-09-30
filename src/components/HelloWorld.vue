<template>
  <div class="translatable-editor mt-5 ml-5">
    <v-text-field
      v-model.lazy="inputVal"
      @change="submitTextChange()"
      class="text-field"
      placeholder="Enter text"
      :readonly="disabled"
      :label="selectedLang"
      dense
      outlined
    ></v-text-field>
    <v-select
      class="select-lang ml-1"
      v-model="selectedLang"
      :items="langs"
      @change="switchLang"
      dense
      outlined
      append-icon=""
    >
      <template v-slot:selection="{ item }">
        <div class="selection-container">
          {{ item }}
        </div>
      </template>

      <template v-slot:item="{ item }">
        <v-checkbox :input-value="checkLang(item)" disabled></v-checkbox>
        <v-list-item-content>
          {{ item }}
        </v-list-item-content>
      </template>
    </v-select>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    disabled: {
      type: Boolean,
      required: true,
    },
    value: {
      type: Array,
      default() {
        return [
          { lang: "ru", text: "" },
          { lang: "de", text: "" },
          { lang: "en", text: "" },
          { lang: "he", text: "" },
        ];
      },
    },
  },
  emits: ["update:value"],
  data() {
    return {
      list: this.value,
      langs: ["ru", "de", "en", "he"],
      selectedLang: "ru",
      inputVal: "",
    };
  },
  watch: {
    value(newValue) {
      this.list = newValue;
      this.inputVal = this.list.find((item) => item.lang == this.selectedLang).text;
    },
  },
  mounted() {
    this.inputVal = this.list[0].text;
  },
  methods: {
    submitTextChange() {
      const itemToUpdate = this.list.find((item) => item.lang == this.selectedLang);
      if (itemToUpdate == undefined) {
        this.list = [
          ...this.list.concat({ lang: this.selectedLang, text: this.inputVal }),
        ];
        this.$emit("input", this.list);
        return;
      }
      this.list = this.list.map((item) =>
        item.lang == this.selectedLang ? { ...item, text: this.inputVal } : item
      );
      this.$emit("input", this.list);
    },
    switchLang() {
      const itemToUpdate = this.list.find((item) => item.lang == this.selectedLang);
      this.inputVal = itemToUpdate != undefined ? itemToUpdate.text : "";
    },
    checkLang(lang) {
      const langToCheck = this.list.find((item) => item.lang == lang && item.text !== "");
      return langToCheck ? true : false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.translatable-editor {
  width: 350px;
  display: flex;
}

.select-lang {
  flex: 0px;
  height: 200px;
}

/* Checkbox style */
.theme--light.v-input--is-disabled {
  color: rgb(0, 142, 225);
}
.v-list-item {
  height: 20px !important;
}
/* select style */
#app > div > div.translatable-editor.mt-5.ml-5 > div.v-input.select-lang.ml-1.v-input--is-label-active.v-input--is-dirty.v-input--dense.theme--light.v-text-field.v-text-field--is-booted.v-text-field--enclosed.v-text-field--outlined.v-select > div > div.v-input__slot {
  width: 40px !important;
}
</style>
