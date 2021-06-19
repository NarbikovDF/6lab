<template>
    <Page>
        <ActionBar title="Персонажи ''Игры Престолов''"/>
            <StackLayout>
              <StackLayout>
                <label> Имя: {{this.name}}</label>
                <label> Пол: {{this.gender}}</label>
                <label> Культура: {{this.culture}}</label>
                <label> Место и дата рождения: {{this.born}}</label>
                <label> Место и дата смерти: {{this.died}}</label>
                <label> Отец: {{this.father}}</label>
                <label> Мать: {{this.mother}}</label>
                <label> Супруг/a: {{this.spouse}}</label>     
             </StackLayout>
              <StackLayout>
               <TextField class="input" v-model="id" hint="Введите ID персонажа"  @Push= "ReplaceHero()"/>
                <Button text='Найти' class="ButtFind" @tap="view()"/>
              </StackLayout>
            </StackLayout>
    </Page>
</template>

<script >
import { Http } from '@nativescript/core'
import * as ApplicationSettings from "@nativescript/core/application-settings";
  export default {
    data() {
      return {
        id: '',
        name: '',
        gender: '',
        culture: '',
        born: '',
        died: '',
        father: '',
        mother: '', 
        spouse: '',
        characters: []
      }
    
    },
    
    methods: {
      ReplaceHero() {
        if(this.id != ''){
          this.msg = this.id
        }
      },
 
      view (){
        Http.getString('https://anapioficeandfire.com/api/characters/' + this.id + '/').then(
          (result) => {
            this.result = JSON.parse(result)
            this.name = this.result.name
            this.gender = this.result.gender 
            this.culture = this.result.culture
            this.born = this.result.born
            this.died = this.result.died
            this.father = this.result.father
            this.mother = this.result.mother
            this.spouse = this.result.spouse
          }
        )
      }
    }
  }
  
</script>

<style scoped>
ActionBar {
  background-color: black;
  color: rgb(255, 255, 255);
  }
  .text{
    text-align: center;
  }
  .ButtFind{
    color: rgb(255, 255, 255);
    background-color: black;
  }
  .ButtFind:active{
    color: black;
    background-color: rgb(255, 255, 255);
  }
</style>