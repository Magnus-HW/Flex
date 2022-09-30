<template>
  <v-app>
    <!-- <HelloWorld v-model="propList" :disabled="disableInput" /> -->
    <content-editable :="propList"></content-editable>
    <!-- <v-btn @click="switchWritable()">switchWritable</v-btn>
    <v-btn @click="switchList()">SwitchList</v-btn>
    <div>
      <div v-for="item in propList" :key="item.lang">{{item.lang}} {{item.text}}</div>
    </div> -->
  </v-app>
</template>

<script>
import ContentEditable from "./components/content-editable.vue";

export default {
  name: "App",

  components: {
    ContentEditable,
  },

  data() {
    return {
      disableInput: false,
      firstList: {
        // может быть или не быть в зависимости от поля. Определяет опубликованность данной языковой версии в целом
        _published: ["ru", "de", "he"],
        // контент может быть поделен на разделы по ключам
        langs : {
          ru: {
            title : "RU Text",
            body: "RU Text",
            keywords: ["Key1", "Key2"],
            full_text: "RU Full_-_text"
          },
          de: {
            title : "DE Text",
            body: "DE Text",
            keywords: ["DE Key1", "DE Key2"],
            full_text: "DE Full_-_text"
          },
          he: {
            title : "HE Text",
            body: "HE Text",
            keywords: ["HE Key1", "HE Key2"],
            full_text: "HE Full_-_text"
          },
        }
      },
      secondList: {
        // может быть или не быть в зависимости от поля. Определяет опубликованность данной языковой версии в целом
        _published: ["ru", "de", "he"],
        // контент может быть поделен на разделы по ключам
        langs : {
          ru: {
            title : "NEW RU Text",
            body: "NEW RU Text",
            keywords: ["NEW Key1", "NEW Key2"],
            full_text: "NEW RU Full_-_text"
          },
          de: {
            title : "NEW DE Text",
            body: "NEW DE Text",
            keywords: ["NEW DE Key1", "NEW DE Key2"],
            full_text: "NEW DE Full_-_text"
          },
          he: {
            title : "NEW HE Text",
            body: "NEW HE Text",
            keywords: ["NEW HE Key1", " NEW HE Key2"],
            full_text: "NEW HE Full_-_text"
          },
        }
      },
      propList: {
        // может быть или не быть в зависимости от поля. Определяет опубликованность данной языковой версии в целом
        _published: ["ru", "de", "he"],
        // контент может быть поделен на разделы по ключам
        langs : {
          ru: {
            title : "RU Text",
            body: "RU Text",
            keywords: ["Key1", "Key2"],
            full_text: "RU Full_-_text"
          },
          de: {
            title : "DE Text",
            body: "DE Text",
            keywords: ["DE Key1", "DE Key2"],
            full_text: "DE Full_-_text"
          },
          he: {
            title : "HE Text",
            body: "HE Text",
            keywords: ["HE Key1", "HE Key2"],
            full_text: "HE Full_-_text"
          },
        }
      },
    }
  },
  mounted() {
    this.propList = this.firstList;
  },
  methods: {
    switchWritable() {
      this.disableInput = !this.disableInput;
      console.log(this.disabledInput);
    },
    switchList() {
      this.propList = this.propList == this.firstList ? this.secondList : this.firstList;
      console.log(this.propList == this.firstList);
    },
  },
};
</script>

<style scoped>
.v-btn {
  width: 150px;
}
</style>
