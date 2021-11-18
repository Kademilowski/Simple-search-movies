<template>

    <div id="3app" class="col-10 offset-1 mb-4 mt-4">

        <searchM @mes-from-search='receivedSearch'/>
     
        <table class="table table-striped">
            <thead>
                <tr>  
                    <th>#</th>   
                    <th>Title</th> 
                    <th>Production Year</th> 
                    <th>Cast</th> 
                    <th>Genre</th> 
                </tr>
            </thead>
            <tbody>
             
                <tr  v-for="(film,index) in filterMovies.slice(0, RowsToShow)" :key="index"  >    
                    <td>{{index + 1}}</td> 
                    <td>{{film.title}}</td> 
                    <td>{{film.year}}</td> 
                    <td>
                       <div v-for="(castFilm,indexCast) in film.cast" :key="indexCast">
                           <span v-if="castFilm === null"> </span>
                           <span v-else>{{castFilm}}</span>
                        </div>
                     </td> 
                   
                   <td>
                   <div v-for="(genresFilm,indexGenres) in film.genres" :key="indexGenres">
                       <span v-if="genresFilm === null">brak</span>
                       <span v-else>{{genresFilm}}</span>
                    </div>
                    </td>
                     
                </tr>
            </tbody>
        </table>
      
        <div class="offset-10">
             <button class="btn btn-primary" @click="RowsToShow += 10">Pokaż więcej</button>
         </div>

    </div>
    
</template>

<script>

import movies from '../data/movies.json'
import searchM from '../components/searchMovie'

export default {
    
    name: '',

    components: {
        searchM
    },

    data(){
        return{
            RowsToShow: 10,
            filterMovies: movies,
            inputYearFromm: 1,
            inputYearToo: 3000,
            
      }
    },

    methods:{

         receivedSearch: function(arg1){
            this.filterMovies = arg1;
           
        }

    }


}

</script>

<style scoped>

</style>