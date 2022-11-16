<script setup>
import CardAlbum from '@/components/CardAlbum.vue'

</script>

<template>
    <div class="min-h-screen flex flex-col">
      <header class="h-32 text-2xl w-full flex-none -ml-full shadow-lg bg-gradient-to-br from-teal-600 to-cyan-400">
        <div class="p-4 h-32 text-2xl w-full flex-none -ml-full rounded-2xl transform shadow-lg bg-gradient-to-br from-cyan-400 to-teal-600 -rotate-1 sm:-rotate-1"> Disco Sciences-U (v3)</div>
      </header>
      
    
      <div class="flex flex-row ">
         <div class=" px-8 bg-cyan-100 "> <!-- left filter panel -->
          <div class="mt-2 basis-1/4">

              <div class="overflow-hidden shadow sm:rounded-md">
                  <div class="bg-white p-6 w-64 h-96">
                    
                    <fieldset>
                      <legend class="sr-only">Filtres</legend>
                      <div class="text-base font-medium text-gray-900" aria-hidden="true">Filtres</div>
                        <div class="mt-4 space-y-4">

                          <div class="flex items-start">
                            <div class="flex h-5 items-center">
                              <input 
                                id="comments" 
                                name="comments" 
                                type="checkbox" 
                                class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
                               
                              >
                            </div>
                            <div class="ml-3 text-sm">
                              <label for="comments" class="font-medium text-cyan-700">In stock only</label>
                            </div>
                           
                          </div>
     
                        </div>
                        <label for="sortBy" class="block text-sm mt-2 font-medium text-cyan-700">Sort by</label>
                        <select id="sortBy" name="sortBy" autocomplete="country-name" class="mt-1 block w-full rounded-md border border-gray-300 bg-white py-2 px-3 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm">
                          <option>Year     </option>
                          <option>Pitchfork</option>
                        </select>
                    </fieldset>
                   
                  </div>
               
              </div>
          </div>
        </div>

        <main class="bg-white py-5 ml-6 basis-auto">
            <!-- component -->
            <CardAlbum />
            <CardAlbum />
        </main>
      </div>
    
      <footer class="bg-gray-100">Pied</footer>

    </div>
</template>

<style scoped>

</style>
