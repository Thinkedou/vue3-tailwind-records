<script setup>
import {ref} from 'vue'
import {records} from './assets/static/js/allRecords'


import CardRecords from './components/CardRecords.vue';


const title = ref('Nom de la page')

console.log(title.value)

const localRecords = ref(records)






const increaseStockHandler = (data)=>{
  console.warn('👂 Album Id::', data) // ici je récupère l'id de l'album
  // donc je dois attraper le bon album dans localRecords 
  const album = localRecords.value.find((album)=>album.id===data)
  album.stock++
  
}

// ref pour filtres (éléments de formulaire, branchés avec v-model)
const stockOnly = ref(false)
const sortOptions = ref("Pitchfork")


const stockOnlyHandler = ()=>{
  // si la personne à coché: stock only 
  if(stockOnly.value){
    localRecords.value = localRecords.value.filter((album)=>album.stock>0)
  }else{
    // si la personne a décoché ou jamais coché stockOnly
    localRecords.value = records
  }
  //console.log('Hey CHANGE',stockOnly.value)
}

const handleSort = ()=>{

  if(sortOptions.value=='Pitchfork'){
    localRecords.value.sort((a, b) => a.pitchforkPos - b.pitchforkPos);
  }

  if(sortOptions.value=='Year'){
    localRecords.value.sort((a, b)=> Number(b.year) - Number(a.year));
  }
   console.log(sortOptions.value)
}
const handleFav  = (albumId)=>{
  // soit je passe par l'id et il me faut donc récupérer le bon album 
  // soit je passe directement l'album en param 
  const album = localRecords.value.find((album)=>album.id===albumId)
  console.log('ajout en favori album:', album)
  // J'ajoute à la volé, dynamiquement, un nouvel attribut: "isFav"
  album.isFav = true
}


</script>

<template>
    <div class="min-h-screen flex flex-col">
      <header class="h-32 text-2xl w-full flex-none -ml-full shadow-lg bg-gradient-to-br from-teal-600 to-cyan-400">
        <div class="p-4 h-32 text-2xl w-full flex-none -ml-full rounded-2xl transform shadow-lg bg-gradient-to-br from-cyan-400 to-teal-600 -rotate-1 sm:-rotate-1"> Disco CCI (v3)</div>
      </header>
      
    
      <div class="flex flex-row ">
         <div class=" px-8 bg-cyan-100 "> <!-- left filter panel -->
          <div class="mt-2 basis-1/4">

              <div class="overflow-hidden shadow sm:rounded-md">
                  <div class="bg-white p-6 w-64 h-96">
                    
                    <fieldset>
                      <legend class="sr-only">Filtres</legend>
                      <div class="text-base font-medium text-gray-900" aria-hidden="true">Filtres (3)</div>
                        <div class="mt-4 space-y-4">

                          <div class="flex items-start">
                            <div class="flex h-5 items-center">
                              <input 
                                id="comments" 
                                name="comments" 
                                type="checkbox" 
                                @change="stockOnlyHandler"
                                v-model="stockOnly"
                                class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
                              >
                            </div>
                            <div class="ml-3 text-sm">
                              <label for="comments" class="font-medium text-cyan-700">In stock only</label>
                            </div>
                          </div>
     
                        </div>
                        <label for="sortBy" class="block text-sm mt-2 font-medium text-cyan-700">Sort by</label>
                        <select 
                            v-model="sortOptions"
                            id="sortBy"
                            name="sortBy" 
                            @change="handleSort"
                            class="mt-1 block w-full rounded-md border border-gray-300 bg-white py-2 px-3 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm">
                          <option >Year</option>
                          <option >Pitchfork</option>
                        </select>
                    </fieldset>
                    {{ sortOptions }}
                  </div>
               
              </div>
          </div>
        </div>

        <main class="bg-white py-5 ml-6 basis-auto">

          <CardRecords 
            v-for="album in localRecords"
              :key="album.id"
              :title='album.title'
              :artist='album.artist'
              :cover-url="album.coverUrl"
              :stock="album.stock"
              :pitchfork-pos="album.pitchforkPos"
              :year="album.year"
              :id = "album.id"
              :comment="album.comment"
              :is-fav="album.isFav"
              @onIncreaseStock="increaseStockHandler"
              @click="handleFav(album.id)"
          />

        </main>
      </div>
    
      <footer class="bg-gray-100">

      </footer>

    </div>
</template>

<style scoped>

</style>
