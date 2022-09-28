<template>
  <div class="translatable-editor">
    <v-text-field
          v-model.lazy="inputVal"
          @change="submitTextChange()"
          class="text-field"
          placeholder="Enter text"
          solo
    ></v-text-field>
    <v-select
        class="select-lang"
        v-model="selectedLang"
        :items="langs"
        @change="switchLang"
        label="ru"
        solo
    ></v-select>
    
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      list : [
        { lang: "ru", text: "Страница" },
        { lang: "de", text: "Seite" },
        { lang: "he", text: "עמוד" },
      ],
      langs: ["ru", "de", "en", "he"],
      selectedLang: "ru",
      inputVal: ""
    }
  },
  watch: {

  },
  mounted() {
    this.inputVal = this.list[0].text
  },
  methods: {
    submitTextChange() {
      const itemToUpdate = this.list.find(item => item.lang == this.selectedLang)
      if(itemToUpdate == undefined) {
        this.list = [...this.list.concat({lang: this.selectedLang, text: this.inputVal})]
        return
      }
      this.list = this.list.map(item => item.lang == this.selectedLang ? {...item, text: this.inputVal} : item)
    },
    switchLang() {
      const itemToUpdate  = this.list.find(item => item.lang == this.selectedLang)
      this.inputVal = itemToUpdate != undefined ? itemToUpdate.text : ""
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.translatable-editor {
  width: 350px;
  display: flex;
}
.text-field {
  
}
.select-lang {
  /* width: 50px; */
  flex: 0px;
  display: inline-block;
}
</style>
