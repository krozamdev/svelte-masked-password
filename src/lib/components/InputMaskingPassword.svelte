<script lang="ts">
  import { onDestroy, onMount } from "svelte";
  import { applyMaskedInput } from "@krozamdev/masked-password";

  export let onChangeEvent: (originalValue: string) => void;
  export let maskCharacter: string = "•";
  export let showPassword: boolean = false;

  let inputRef: HTMLInputElement | null = null;
  let maskedInputRef: ReturnType<typeof applyMaskedInput> | null = null;

  // apply the masked input logic on mount
  onMount(() => {
    if (inputRef) {
      maskedInputRef = applyMaskedInput(inputRef, {
        character: maskCharacter,
        onChange: onChangeEvent,
      });
    }

    // cleanup on destroy
    onDestroy(() => {
      if (maskedInputRef) {
        maskedInputRef.purgeDestroy();
      }
    });
  });

  // react to show password changes
  $: {
    if (maskedInputRef) {
      if (showPassword) {
        maskedInputRef.destroy();
      } else {
        maskedInputRef.addEvent();
      }
    }
  }
</script>

<input bind:this={inputRef} {...$$restProps} />
