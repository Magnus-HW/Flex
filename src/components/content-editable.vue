<template>
  <div class="content-editable">
    <v-toolbar>
      <template v-slot:extension>
        <v-tabs v-model="tab" align-with-title>
          <v-tabs-slider color="yellow"></v-tabs-slider>

          <v-tab v-for="item in existedLangs" :key="item">
            {{ item }}
          </v-tab>
        </v-tabs>

        <v-select
          class="select-lang ml-1"
          v-model="newLang"
          :items="unexistedLangs"
          @change="addLangToExisted"
          dense
          outlined
          append-icon=""
        >
          <template v-slot:selection="{ item }">
            <div class="selection-container">
              {{ item }}
            </div>
          </template>
        </v-select>

      </template>
    </v-toolbar>

    <v-tabs-items v-model="tab">
      <v-tab-item v-for="lang in existedLangs" :key="lang">
        <v-card flat> 
          <v-card-text>
           <editable-input :propValue="content.langs[lang]?.title" :disabled="false"></editable-input>
            <p>{{ content.langs[lang]?.title }}</p>
            <p>{{ content.langs[lang]?.body }}</p>
            <p>{{ content.langs[lang]?.keywords }}</p>
            <p>{{ content.langs[lang]?.full_text }}</p>
          </v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
  </div>
</template>

<script>
import EditableInput from "@/components/editable-input";
export default {
  components: {
    EditableInput
  },
  props: {
    propContent: {
      type: Object,
      reqired: true,
    },
  },
  data() {
    return {
      tab: null,
      allLangs: ["ru", "de", "en", "he"],
      existedLangs: [],
      unexistedLangs: [],
      newLang: "",
      content: {
        _published: [],
        langs: [],
      },
    };
  },
  watch: {
    propContent(newContent) {
      this.content = newContent;
    },
  },
  mounted() {
    this.content = this.propContent;
    this.existedLangs = Object.keys(this.content.langs);
    this.unexistedLangs = this.allLangs.filter((lang) =>
      !this.existedLangs.includes(lang)
    );
    console.log(this.tab);
  },
  methods: {
    addLangToExisted() {
      this.existedLangs.push(this.newLang)
      this.tab = this.existedLangs.length-1
    }
  },
};
</script>

<style scoped></style>
