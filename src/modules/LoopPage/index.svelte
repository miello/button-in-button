<script lang="ts">
  import { onMount } from "svelte";
  import Button from "../../components/Button/index.svelte";
  import type { ButtonProps } from "../../components/Button/types";

  const MAX_BUTTON_LIST = 10;
  const GAP_BETWEEN_BUTTONS = 75;

  let time: number = 0;

  let buttonList: Omit<ButtonProps, "currentTime">[] = [];

  const handleFrame = () => {
    if (time % GAP_BETWEEN_BUTTONS === 0) {
      if (buttonList.length >= MAX_BUTTON_LIST) {
        buttonList.pop();
      }
      buttonList = [
        {
          id: Math.random(),
          startTime: time,
        },
        ...buttonList,
      ];
    }
    time++;
    requestAnimationFrame(handleFrame);
  };

  onMount(() => {
    requestAnimationFrame(handleFrame);
  });
</script>

<div class="parent">
  {#each buttonList as button (button.id)}
    <Button startTime={button.startTime} currentTime={time}>
      <a
        href="https://www.youtube.com/watch?v=PzqQSOaCcnw"
        target="_blank"
        referrerpolicy="no-referrer"
        class="link"
      >
        Click &nbsp; Me 👆
      </a>
    </Button>
  {/each}
</div>

<style>
  .link {
    text-decoration: none;
    color: black;
  }

  .parent {
    overflow: hidden;
    perspective: 1000px;
    perspective-origin: center;
    min-height: 100vh;
    position: relative;
  }
</style>
