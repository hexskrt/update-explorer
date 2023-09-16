<template>
  <!-- footer -->
  <footer
    class="flex items-center h-12 mt-5 text-sm bg-gray-100 dark:bg-[#171d30] py-2 z-10 w-full"
  >
    <div class="flex flex-1">
     ©&nbsp;
      <a
        class="link link-primary no-underline"
        href="https://hexnodes.co"
        target="_blank"
        rel="noopener noreferrer"
        >Hexnodes&nbsp;</a
      >
      {{ new Date().getFullYear() }}&nbsp;All Source Based Ping.Pub
    </div>
    <div
      class="hidden md:!block"
    >
      <a
        class="link link-primary no-underline mr-4"
        href="https://github.com/ping-pub/explorer/blob/master/LICENSE"
        target="noopener noreferrer"
        >License</a
      >
      <a
        class="link link-primary no-underline"
        href="https://github.com/ping-pub/explorer"
        target="noopener noreferrer"
        >Github</a
      >
    </div>
  </footer>
</template>