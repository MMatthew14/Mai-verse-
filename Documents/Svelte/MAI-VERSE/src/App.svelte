<script>
  import { onMount } from 'svelte';
  import Header from './Header.svelte';
  import ImageGrid from './ImageGrid.svelte';
  import ImageModal from './ImageModal.svelte';
 
  //props
 
  
  // State
  let isDarkMode = false;
  let selectedCharacter = null;
  let selectedImage = null;
  let isModalOpen = false;
  
  // Image data structure
  const imageData = [
    {
      id: 1,
      src: "/placeholder.svg?height=400&width=300",
      alt: "Sakurajima Mai in bunny girl outfit",
      character: "mai",
      tags: ["bunny", "uniform"]
    },
    {
      id: 2,
      src: "/placeholder.svg?height=400&width=300",
      alt: "Sakurajima Mai in school uniform",
      character: "mai",
      tags: ["school", "uniform"]
    },
    {
      id: 3,
      src: "/placeholder.svg?height=400&width=300",
      alt: "Futaba Rio with glasses",
      character: "rio",
      tags: ["glasses", "lab coat"]
    },
    {
      id: 4,
      src: "/placeholder.svg?height=400&width=300",
      alt: "Koga Tomoe smiling",
      character: "tomoe",
      tags: ["smile", "casual"]
    },
    {
      id: 5,
      src: "/placeholder.svg?height=400&width=300",
      alt: "Toyohama Nodoka in idol outfit",
      character: "nodoka",
      tags: ["idol", "performance"]
    },
    {
      id: 6,
      src: "/placeholder.svg?height=400&width=300",
      alt: "Makinohara Shouko at the beach",
      character: "shouko",
      tags: ["beach", "summer"]
    },
    {
      id: 7,
      src: "/placeholder.svg?height=400&width=300",
      alt: "Sakurajima Mai in casual clothes",
      character: "mai",
      tags: ["casual", "shopping"]
    },
    {
      id: 8,
      src: "/placeholder.svg?height=400&width=300",
      alt: "Futaba Rio in school uniform",
      character: "rio",
      tags: ["school", "uniform"]
    },
    {
      id: 9,
      src: "/placeholder.svg?height=400&width=300",
      alt: "Sakurajima Mai and Azusagawa Sakuta",
      character: "mai",
      tags: ["couple", "sakuta"]
    },
    {
      id: 10,
      src: "/placeholder.svg?height=400&width=300",
      alt: "Makinohara Shouko smiling",
      character: "shouko",
      tags: ["smile", "school"]
    },
    {
      id: 11,
      src: "/placeholder.svg?height=400&width=300",
      alt: "Koga Tomoe with phone",
      character: "tomoe",
      tags: ["phone", "school"]
    },
    {
      id: 12,
      src: "/placeholder.svg?height=400&width=300",
      alt: "Toyohama Nodoka with headphones",
      character: "nodoka",
      tags: ["headphones", "music"]
    }
  ];
  
  // Reactive declaration for filtered images
  $: filteredImages = selectedCharacter 
    ? imageData.filter(img => img.character === selectedCharacter)
    : imageData;
  
  // Functions
  function toggleDarkMode() {
    isDarkMode = !isDarkMode;
    if (isDarkMode) {
      document.documentElement.classList.add('dark');
    } else {
      document.documentElement.classList.remove('dark');
    }
  }
  
  function selectCharacter(character) {
    selectedCharacter = character === selectedCharacter ? null : character;
  }
  
  function openModal(image) {
    selectedImage = image;
    isModalOpen = true;
  }
  
  function closeModal() {
    isModalOpen = false;
    selectedImage = null;
  }
  
  // Initialize dark mode based on user preference
  onMount(() => {
    const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
    isDarkMode = prefersDark;
    if (isDarkMode) {
      document.documentElement.classList.add('dark');
    }
  });
</script>

<div class={`min-h-screen ${isDarkMode ? 'dark' : ''}`}>
  <div class="min-h-screen bg-gradient-to-b from-purple-50 to-blue-50 dark:from-gray-900 dark:to-gray-950 transition-colors duration-200">
    <Header 
      {isDarkMode} 
      {toggleDarkMode} 
      {selectedCharacter} 
      {selectCharacter} 
    />
    
    <main class="container px-4 py-6 mx-auto md:py-10">
      <div class="flex flex-col items-center justify-center mb-8 space-y-2 text-center">
        <h1 class="text-3xl font-bold tracking-tight text-purple-800 dark:text-purple-300 sm:text-4xl">
          Seishun Buta Yarou Imageboard
        </h1>
        <p class="max-w-[700px] text-gray-600 dark:text-gray-400">
          A collection of images featuring Sakurajima Mai and other characters from Rascal Does Not Dream of Bunny Girl Senpai
        </p>
      </div>
      
      <ImageGrid 
        images={filteredImages} 
        onImageClick={openModal} 
      />
    </main>
    
    <footer class="py-6 text-center text-sm text-gray-500 dark:text-gray-400">
      © {new Date().getFullYear()} Seishun Buta Yarou Imageboard. All rights reserved.
    </footer>
  </div>
  
  {#if isModalOpen && selectedImage}
    <ImageModal image={selectedImage} onClose={closeModal} />
  {/if}
</div>

<style>
  :global(html) {
    font-family: Inter, system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  }
  
  :global(.dark) {
    --background: 240 10% 3.9%;
    --foreground: 0 0% 98%;
    --card: 240 10% 3.9%;
    --card-foreground: 0 0% 98%;
    --primary: 270 76% 60%;
    --primary-foreground: 0 0% 98%;
    --secondary: 240 3.7% 15.9%;
    --secondary-foreground: 0 0% 98%;
    --muted: 240 3.7% 15.9%;
    --muted-foreground: 240 5% 64.9%;
    --border: 240 3.7% 15.9%;
  }
  
  :global(body) {
    margin: 0;
    padding: 0;
  }
  
  :global(*) {
    box-sizing: border-box;
  }
</style>