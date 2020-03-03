<template>
<form @submit.prevent="translateIt" class="well">
    <textarea v-model="searchText" cols="10" rows="5" class="form-control" placeholder="Type Something to translate from intended language"></textarea>
       <p>{{ searchText }} </p>
        <select class="form-control" v-model="translateTo">
     <option v-for="(lang,key) in languages" v-bind:value="key">{{ lang }}</option>
        </select>
        <br>
        <div class="text-left">
            <strong>Detected Language : {{ languages [translateTo]}} </strong>
        </div>
        <br>
        <button type="submit" class="btn btn-primary btn-block">Translate It</button>
</form>
</template>

<script>
import axios from "axios"
export default {
    data(){
    return{
      searchText: "",
      languages: {},
      translateTo: "",
        }
    },
    methods: {
        translateIt(){//getting api
            let url = "https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20191017T142651Z.881f6ef4bc5ddc4d.6bcdf4a31a3560e1ead852eb8a7231bfd0c11cbc&text=" +this.searchText+ "&lang="+ this.translateTo
            axios.get(url)
            .then(response =>{
                
                let translatePack = {
                    fromLang: this.languages[response.data.lang.split("-")[0]],
                    toLang : this.languages[this.translateTo],
                    fromText : this.searchText,
                    toText: response.data.text[0]
                 }
            this.$emit("translatedEvent", translatePack)
           }).catch(err=> console.log(err))
        }
    },
  created(){
            axios.get("https://translate.yandex.net/api/v1.5/tr.json/getLangs?key=trnsl.1.1.20191017T142651Z.881f6ef4bc5ddc4d.6bcdf4a31a3560e1ead852eb8a7231bfd0c11cbc&ui=eng")
      .then(response => {
          this.languages = response.data.langs
        })
  }
}
</script>

<style>
.well{
  background-color: white;  
}
</style>