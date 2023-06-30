<script lang="ts">
  export let startTime: number;
  export let currentTime: number;

  let minShift = -5000;
  let maxShift = 1000;

  let shift = -2000;

  const BezierEasing = (time: number) => {
    return time * time * (3.0 - 2.0 * time);
  };

  const shiftButton = () => {
    if (shift >= maxShift) return;
    shift =
      minShift +
      (maxShift - minShift) *
        BezierEasing(Math.min(1.0, (currentTime - startTime) / 250));
  };

  $: currentTime, shiftButton();
</script>

<button
  class="btn"
  style={`
    transform: translate(-50%, -50%) translateZ(${shift}px) !important;
    transform-style: preserve-3d;
    --webkit-transform: translate(-50%, -50%) translateZ(${shift}px) !important;
    --moz-transform: translate(-50%, -50%) translateZ(${shift}px) !important;
    --ms-transform: translate(-50%, -50%) translateZ(${shift}px) !important;
    --o-transform: translate(-50%, -50%) translateZ(${shift}px) !important;
    z-index: 99`}
>
  <slot />
</button>

<style>
  .btn {
    position: absolute;
    padding: 8px 24px;

    background-color: transparent;
    border: 1px #111111 solid;
    border-radius: 16px;
    cursor: pointer;

    top: 50%;
    left: 50%;

    font-size: 3rem;
  }
</style>
