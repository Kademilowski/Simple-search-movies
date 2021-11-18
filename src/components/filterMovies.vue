<template>
<div>
    <div id="filterGenres" class="mb-5 mt-2">
        
        <h2>Filmy według gatunku</h2>
        <button class="btn btn-primary" @click="hiddenGenres = !hiddenGenres">Pokaż/Schowaj</button>
        <div v-if=hiddenGenres >
            <ul class="list-group list-group-flush" v-for="(genre, index) in genresMoviesL" :key="index">
                <li class="list-group-item">{{genre}}</li>
                    <ul v-for="(movie, index1) in GenresMovies(genre)"  :key="index1">
                        <li class="list-group-item">{{index1 +1 }}. {{ movie.title }}</li>
                    </ul>
            </ul>
        </div>
        
    </div>

    <div id="filterCasts" class="mb-5">
    
       <h2>Filmy według aktorów</h2>
       <button class="btn btn-primary" @click="hiddenCast = !hiddenCast" >Pokaż/Schowaj</button>
        <div v-if=hiddenCast >
            <ul v-for="(cast,index) in castMoviesL" :key="index" class="list-group list-group-flush">
                    <li class="list-group-item"> {{cast}}</li>  
                    <ul v-for="(movie, index1) in CastMovies(cast)"  :key="index1">
                        <li class="list-group-item">{{index1+1}}. {{ movie.title }}</li>
                    </ul>
               
            </ul>
        </div>
    </div>

</div>
</template>



<script>

import filmy from '../data/movies.json'
import {_} from 'vue-underscore'


export default {
   

    data(){
        return{
            items: filmy,
            Movies100: [],
            genresMoviesL: [],
            castMoviesL: [],
            hiddenGenres: true,
            hiddenCast: true
           
        }
    },

    methods:{
           MoviesByGenres: function(){
                let TmpMovies = [];
                
                TmpMovies =  _.flatten(_.pluck(this.Movies100, 'genres'));
                this.genresMoviesL = _.uniq(TmpMovies);
                

           },

            MoviesByCast: function(){
                let TmpMovies = [];

                TmpMovies = _.flatten(_.pluck(this.Movies100, 'cast'));
                this.castMoviesL = _.uniq(TmpMovies);
               
           },


            GenresMovies: function(genres){
                let varTmp = [];

                _.each(this.Movies100, (movie)=>{
                    if(_.contains(movie.genres, genres) === true){
                        varTmp.push(movie);
                    }
                });

                return varTmp;
            },

            CastMovies: function(cast){
                let varTmp = [];

                _.each(this.Movies100, (movie)=>{
                    if(_.contains(movie.cast, cast) === true){
                        varTmp.push(movie);
                    }
                });
                
                return varTmp;
            },
        
    },


        mounted(){
            //this.Movies100 = _.last(this.items, 100);
            this.Movies100 = this.items.slice(0,100);
            this.MoviesByGenres();
            this.MoviesByCast();
        }

}

</script>