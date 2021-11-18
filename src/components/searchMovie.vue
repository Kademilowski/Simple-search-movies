<template>
    <div class="mb-5">
        <h1> Baza filmów </h1>
            
                <form>
                  <div class="form-group">
                      <div>
                        <label>Tytuł</label>
                        <input type="text" class="form-control col-6" placeholder="Podaj tytul lub fragment tutyulu filmu"
                         v-model="Title"/>
                      </div>
                      <div >
                        <label style="display:'block';">Rok Produkcji od:</label>
                        <input type="number" class="form-control col-6" 
                        min=0 oninput="validity.valid||(value='');"
                        placeholder="liczba naturalna z przedziału 1900 - 2019" 
                         v-model="YearProductionFrom"/>
                      </div>
                      <div >
                        <label>Rok Produkcji do:</label>
                        <input type="number" class="form-control col-6" 
                        min=0 oninput="validity.valid||(value='');"
                        placeholder="liczba naturalna z przedziału 1900 - 2019" 
                         v-model="YearProductionTo" />
                      </div>
                      <div>
                      <label>Obsada</label>
                        <input type="text" class="form-control col-6" 
                        placeholder="Imię i Nazwisko" 
                         v-model="Cast"/>
                      </div>
                   </div>
                </form>
                <button class="btn btn-primary" @click="sendMesToTable()" >Szukaj</button>
            </div>
    
</template>

<script>
import {_} from 'vue-underscore'
import movies from '../data/movies.json'



export default {
    

    data(){
      return{
          inputCast: this.Cast,
          inputYearFrom: this.YearProductionFrom,
          inputYearTo: this.YearProductionTo,
          inputTitle: this.Title,
          items: movies,
          MovieArray: [],
          isYear: false,
          isCast: false,
          isTitle: false
      }
    },

    methods: {
      
        sendMesToTable: function() {
             let tmp = [];

            _.each(this.items, (movie)=>{

                if(_.isEmpty(this.YearProductionFrom) && _.isEmpty(this.YearProductionTo)){
                    this.isYear = true;
                }

                if((_.isEmpty(this.YearProductionFrom) || (parseInt(movie.year)) >= parseInt(this.YearProductionFrom)) && (_.isEmpty(this.YearProductionTo) || (parseInt(movie.year) <= parseInt(this.YearProductionTo)))){
                    this.isYear = true;
                }

                if(movie.title.includes(this.Title) || _.isEmpty(this.Title)){
                    this.isTitle = true;    
                }
                   
            
  
                if(_.isEmpty(this.Cast)){
                    this.isCast = true;
                }

               _.each(movie.cast, (item)=>{
                    if(item.includes(this.Cast))
                        this.isCast = true;
              
                })


                if((this.isYear) && (this.isTitle) && (this.isCast)){
                    tmp.push(movie);
                }   
          
                  this.isYear = false;
                  this.isTitle = false;
                  this.isCast = false;

                })

                

                 this.MovieArray = tmp;

                 this.$emit('mes-from-search', this.MovieArray);
                      
        }
     }
}

</script>


<!-- Stylizowanie -->
<style scoped>

</style>