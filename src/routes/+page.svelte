<script>
  import { page } from '$app/stores';
  import Seo from '$cmp/page/SEO.svelte';

  const links = [
    {
      name: 'Start',
      path: '/start',
    },
    {
      name: 'Bath',
      path: '/bath',
    },
    {
      name: 'Mate',
      path: '/mate',
    },
    {
      name: 'Unexpected',
      path: '/unexpected',
    },
    {
      name: 'Env',
      path: '/env',
    },
  ];
</script>

<Seo
  siteName="BRB Screen"
  canonical="current"
  url="current"
  pageTitle="BRB Screen"
  description="A simple collections of screens to display when you're away from your stream. With a command palette to switch between them. Made with SvelteKit."
  type="website"
  image={{
    url: `${$page.url.origin}/img/brb-screen-home.png`,
    alt: 'BRB Screen home page',
  }}
/>

<main
  class="h-full flex flex-col items-center justify-center gap-24 text-lg text-zinc-200
  bg-[radial-gradient(ellipse_at_center,_var(--tw-gradient-stops))] from-slate-950 to-black"
>
  <header>
    <h1 class="text-3xl font-bold text-center tracking-wide">
      Start using the Command Palette
    </h1>
    <p class="text-sm text-center mt-4">
      Press <span class="font-bold text-zinc-100">Ctrl + P</span> to open
    </p>
  </header>
  <div class="flex flex-col items-center justify-center gap-4">
    <h2 class="text-xl font-semibold tracking-wide">
      Default available screens:
    </h2>
    <div
      class="flex items-center justify-between gap-4 [&_a:hover]:underline [&_a]:underline-offset-2"
    >
      {#each links as link (link.path)}
        <a href={link.path}>{link.name}</a>
      {/each}
    </div>
  </div>
</main>
