<template>
  <main class="min-h-screen bg-gray-800 max-w-screen scroll-smooth">
    <AddNewPost/>  
  </main>
</template>

<style>
/* Scrollbar */
::-webkit-scrollbar {
  width: 6px;
}
::-webkit-scrollbar-track {
  background:#1e293b;
}
::-webkit-scrollbar-thumb {
  background:#334155;
}

/* Selection */
::selection {
background: #334155; /* Safari */
}
::-moz-selection {
background: #334155; /* Firefox */
}
</style>