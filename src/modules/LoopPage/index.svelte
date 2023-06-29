<script lang="ts">
  import { onMount } from "svelte";
  import Button from "../../components/Button/index.svelte";
  import type { ButtonProps } from "../../components/Button/types";

  const MAX_BUTTON_LIST = 10;
  const GAP_BETWEEN_BUTTONS = 100;

  let time: number = 0;

  const buttonList: Omit<ButtonProps, "currentTime">[] = [];

  const handleFrame = () => {
    if (time % GAP_BETWEEN_BUTTONS === 0) {
      if (buttonList.length >= MAX_BUTTON_LIST) {
        buttonList.shift();
      }
      buttonList.push({
        startTime: time,
      });
      console.log(buttonList);
    }
    time++;
    requestAnimationFrame(handleFrame);
  };

  onMount(() => {
    requestAnimationFrame(handleFrame);
  });
</script>

<div class="parent">
  {#each buttonList as button}
    <Button startTime={button.startTime} currentTime={time}>Click Me 👆</Button>
  {/each}
</div>

<style>
  .parent {
    overflow: hidden;
    perspective: 1000px;
    perspective-origin: center;
    min-height: 100vh;
    position: relative;
  }
</style>
