<template>
  <div>
      <v-app>
          <v-card class="mx-auto mt-10" width="50%">
            <v-card-title>LETTER COMBINATION</v-card-title>
            <v-card-text class="pb-0">
              <v-text-field
              v-model="model"
              type="number"
              hide-spin-buttons
              outlined
              hide-details
              label="Enter Combination"
              ></v-text-field>
            </v-card-text>
            <v-card-actions class="ma-2">
              <v-btn block class="success" type="submit" @click.prevent="generate()">Generate</v-btn>
            </v-card-actions>
          </v-card>
          <v-card v-if="results.length > 0" class="mx-auto mt-10" width="50%">
            <v-card-title>Result</v-card-title>
            <v-card-text class="text--primary font-weight-medium">
              {{results}}
            </v-card-text>
          </v-card>
      </v-app> 
  </div>
</template>

<script>
export default {
  data(){
    return {
      model: '',
      list: {
        1: '   ',
        2: 'abc',
        3: 'def',
        4: 'ghi',
        5: 'jkl',
        6: 'mno',
        7: 'pqrs',
        8: 'tuv',
        9: 'wxyz'
      },
      results: []
    }
  },
  methods: {
    generate(){
      let model = this.model;
      let list = this.list;
      let clean = [];
      for(let i = 0; i < model.length; i++){   
        if(Object.keys(this.list).includes(model[i])){
          clean.push(model[i])
        }
      }
      model = clean.join("")
      this.$set(this, 'model', model);

      let entries = [];
      [...Array(model.length).keys()].forEach(k => {
        entries.push(list[model[k]])
      })

      let final = []

      if(entries.length > 1){
        entries.forEach((value,key) => {
          for(let i = 0; i < value.length; i++){
              function reiterate(key){
                if(entries[key] != undefined){
                  for(let s = 0; s < entries[key].length; s++){
                      final.push(value[i] + entries[key][s])
                  }
                  reiterate(key + 1);
                } 
              }
              reiterate(key + 1);
          }           
        })
      }else{
        final = entries
      }
      this.$set(this, 'results',final)
    }
  }
}
</script>
