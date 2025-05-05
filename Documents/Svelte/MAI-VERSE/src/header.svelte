<script>
  import { slide } from 'svelte/transition';
  
  // Props
  export let isDarkMode;
  export let toggleDarkMode;
  export let selectedCharacter;
  export let selectCharacter;
  
  // State
  let isMenuOpen = false;
  
  // Character data
  const characters = [
    { id: null, name: 'All Images', slug: null },
    { id: 'mai', name: 'Sakurajima Mai', slug: 'mai' },
    { id: 'rio', name: 'Futaba Rio', slug: 'rio' },
    { id: 'tomoe', name: 'Koga Tomoe', slug: 'tomoe' },
    { id: 'nodoka', name: 'Toyohama Nodoka', slug: 'nodoka' },
    { id: 'shouko', name: 'Makinohara Shouko', slug: 'shouko' }
  ];
  
  // Functions
  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }
  
  function handleCharacterSelect(character) {
    selectCharacter(character);
    if (isMenuOpen) isMenuOpen = false;
  }
</script>

<header class="sticky top-0 z-40 w-full border-b bg-white/80 backdrop-blur-sm dark:bg-gray-950/80 dark:border-gray-800 transition-colors duration-200">
  <div class="container flex items-center justify-between h-16 px-4 mx-auto">
    <a href="/" class="flex items-center space-x-2">
      <span class="text-xl font-bold text-purple-700 dark:text-purple-400">Mai Imageboard</span>
    </a>
    
    <nav class="hidden md:flex items-center space-x-6 text-sm font-medium">
      {#each characters as character}
        <button 
          class={`${selectedCharacter === character.slug ? 'text-purple-900 dark:text-purple-300' : 'text-gray-600 dark:text-gray-300'} hover:text-purple-700 dark:hover:text-purple-200`}
          on:click={() => handleCharacterSelect(character.slug)}
        >
          {character.name}
        </button>
      {/each}
    </nav>
    
    <div class="flex items-center space-x-2">
      <button
        class="p-2 rounded-md text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-800"
        aria-label="Toggle theme"
        on:click={toggleDarkMode}
      >
        {#if isDarkMode}
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="12" cy="12" r="5"></circle>
            <line x1="12" y1="1" x2="12" y2="3"></line>
            <line x1="12" y1="21" x2="12" y2="23"></line>
            <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
            <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
            <line x1="1" y1="12" x2="3" y2="12"></line>
            <line x1="21" y1="12" x2="23" y2="12"></line>
            <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"></line>
            <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"></line>
          </svg>
        {:else}
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path>
          </svg>
        {/if}
      </button>
      
      <button
        class="md:hidden p-2 rounded-md text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-800"
        on:click={toggleMenu}
        aria-label="Toggle menu"
      >
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="3" y1="12" x2="21" y2="12"></line>
          <line x1="3" y1="6" x2="21" y2="6"></line>
          <line x1="3" y1="18" x2="21" y2="18"></line>
        </svg>
      </button>
    </div>
  </div>
  
  {#if isMenuOpen}
    <div class="container px-4 pb-4 md:hidden" transition:slide={{ duration: 200 }}>
      <nav class="flex flex-col space-y-3 text-sm font-medium">
        {#each characters as character}
          <button 
            class={`text-left ${selectedCharacter === character.slug ? 'text-purple-900 dark:text-purple-300' : 'text-gray-600 dark:text-gray-300'} hover:text-purple-700 dark:hover:text-purple-200`}
            on:click={() => handleCharacterSelect(character.slug)}
          >
            {character.name}
          </button>
        {/each}
      </nav>
    </div>
  {/if}
</header>