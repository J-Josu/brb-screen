<script lang="ts">
  import type { FormPathLeaves, ZodValidation } from 'sveltekit-superforms';
  import type { SuperForm } from 'sveltekit-superforms/client';
  import { formFieldProxy } from 'sveltekit-superforms/client';
  import type { AnyZodObject, z } from 'zod';

  type T = $$Generic<AnyZodObject>;

  export let form: SuperForm<ZodValidation<T>, unknown>;
  export let field: FormPathLeaves<z.infer<T>>;

  export let label: string;
  export let hint: string | undefined = undefined;
  export let readonly: boolean = false;
  export let autocomplete: string = 'off';

  const { value, errors, constraints } = formFieldProxy(form, field);
</script>

<div class=" mt-2">
  <div class=" flex justify-between text-sm font-medium">
    <label for={field} class=" max-w-fit text-zinc-100">
      {label}
    </label>
    {#if $$slots.oppositeToLabel}
      <slot name="oppositeToLabel" />
    {:else if hint}
      <span class=" text-zinc-500">{hint}</span>
    {/if}
  </div>
  <div class=" flex flex-col gap-2">
    <div class="flex gap-2">
      <input
        type="color"
        id={field}
        name={field}
        {autocomplete}
        {readonly}
        bind:value={$value}
        aria-invalid={!!$errors || undefined}
        {...$constraints}
        {...$$restProps}
        class=" mt-2 block w-16 rounded-md border-none px-[2px] h-auto
        text-zinc-100 bg-zinc-900 shadow-sm
        placeholder:text-zinc-600 
        ring-1 ring-inset ring-blue-900"
      />
      <input
        type="text"
        class=" mt-2 block w-full rounded-md border-none py-1.5
        text-zinc-100 bg-zinc-900 shadow-sm
        placeholder:text-zinc-600 sm:text-sm sm:leading-6
        ring-1 ring-inset ring-blue-900"
        bind:value={$value}
      />
    </div>
    {#if $errors}
      <p class=" text-sm text-red-500">
        {$errors}
      </p>
    {/if}
    {#if $$slots.belowInput}
      <slot name="belowInput" />
    {/if}
  </div>
</div>

<style lang="postcss">
  div:has(div input[required]:not(:read-only)) label::after {
    content: ' *';
    color: red;
  }
  input[type="color"] {
	-webkit-appearance: none;
	border: none;
  @apply bg-zinc-900;
	/* width: 32px;
	height: 32px; */
  /* height: 16px; */
  overflow: visible;
}
input[type="color"]::-webkit-color-swatch-wrapper {
	padding: 0;
  @apply bg-zinc-900;
  padding-block: 2px;
  overflow: visible;
}
input[type="color"]::-webkit-color-swatch {
	border: none;
  @apply rounded;
}
input[type="color"]:focus {
    @apply ring-2 ring-blue-600;
  }
  input:focus {
	  -webkit-appearance: none;
    @apply ring-2 ring-blue-600;
  overflow: visible;
  }
  input:read-only {
    @apply cursor-text bg-zinc-900 ring-zinc-800;
  }
</style>