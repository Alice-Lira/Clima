<script setup>

</script>

<template>
  <div class="h-screen w-screen flex items-center justify-center bg-gray-100">

    <div class="bg-blue-600 w-72 shadow-md rounded-md p-6 space-y-4 text-center">
      <div>
        <h3 class="text-white text-base font-bold">Confira o clima de uma cidade:</h3>
      </div>
      <div class="flex gap-2">
        <input type="text" placeholder="Digite uma cidade"
          class=" focus:outline-none w-full border border-gray-400 rounded placeholder:text-gray-300 px-2 text-base">

        <svg data-slot="icon" fill="none" stroke-width="1.5" stroke="currentColor" viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg" aria-hidden="true"
          class="w-8 text-white bg-blue-300 rounded p-1 hover:bg-blue-200">
          <path stroke-linecap="round" stroke-linejoin="round"
            d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z"></path>
        </svg>
      </div>

      <div class="text-white space-y-1">
        <div class="flex justify-center items-center gap-1">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-geo-alt-fill"
            viewBox="0 0 16 16">
            <path d="M8 16s6-5.686 6-10A6 6 0 0 0 2 6c0 4.314 6 10 6 10m0-7a3 3 0 1 1 0-6 3 3 0 0 1 0 6" />
          </svg>
          <h2 class="font-bold flex">Maringá</h2>
          <img src="" alt="Bandeira do país">
        </div>
        <p class="text-sm"><span>38</span> &deg;C</p>

        <div class="flex">
          <p>Nublado</p>
          <img src="" alt="Condições do tempo">
        </div>

        <div class="flex items-center gap-1 justify-center">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-droplet-fill"
            viewBox="0 0 16 16">
            <path
              d="M8 16a6 6 0 0 0 6-6c0-1.655-1.122-2.904-2.432-4.362C10.254 4.176 8.75 2.503 8 0c0 0-6 5.686-6 10a6 6 0 0 0 6 6M6.646 4.646l.708.708c-.29.29-1.128 1.311-1.907 2.87l-.894-.448c.82-1.641 1.717-2.753 2.093-3.13" />
          </svg>
          <p><span>48%</span></p>
        </div>

        <div class="flex items-center gap-1 justify-center">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-wind"
            viewBox="0 0 16 16">
            <path
              d="M12.5 2A2.5 2.5 0 0 0 10 4.5a.5.5 0 0 1-1 0A3.5 3.5 0 1 1 12.5 8H.5a.5.5 0 0 1 0-1h12a2.5 2.5 0 0 0 0-5m-7 1a1 1 0 0 0-1 1 .5.5 0 0 1-1 0 2 2 0 1 1 2 2h-5a.5.5 0 0 1 0-1h5a1 1 0 0 0 0-2M0 9.5A.5.5 0 0 1 .5 9h10.042a3 3 0 1 1-3 3 .5.5 0 0 1 1 0 2 2 0 1 0 2-2H.5a.5.5 0 0 1-.5-.5" />
          </svg>
          <p><span>3km/h</span></p>
        </div>
      </div>
    </div>
  </div>
</template>
