<script lang="ts">
  import WavyText from '$cmp/WavyText.svelte';
</script>

<div class="h-full bg-black">
  <main
    class="h-full flex flex-col justify-center items-center
  bg-[radial-gradient(ellipse_at_center,_var(--tw-gradient-stops))] from-zinc-800/30 to-slate-950"
  >
    <div
      class="flex flex-col justify-center gap-8 lg:gap-0 lg:grid lg:grid-rows-1 lg:grid-cols-[2fr,auto] place-items-center h-full text-white"
    >
      <WavyText text={['Fui al baño,', 'en 5 mins', 'regreso...']} />
      <img
        src="/img/bath.png"
        alt=""
        class=" max-h-52 lg:max-h-none lg:w-auto"
      />
    </div>
  </main>
</div>

<style>
  main {
    font-family: RampartOne, cursive;
  }
</style>
