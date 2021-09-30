<script lang="ts">
  import { createEventDispatcher } from "svelte";
  type IButtonDirection = "forward" | "backward";

  export let buttonDirection: IButtonDirection;
  const dispatch = createEventDispatcher();

  let buttonContent: string;
  if (buttonDirection === "backward") {
    buttonContent = "<<";
  } else if (buttonDirection === "forward") {
    buttonContent = ">>";
  }

  function handleClick(event: MouseEvent) {
    dispatch("slideButtonNotify", buttonDirection);
    event.stopPropagation();
  }
</script>

<div on:click={handleClick} class={`wrapper ${buttonDirection}`}>
  <div class="button">
    <strong>{buttonContent}</strong>
  </div>
</div>

<style>
  .button {
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    background-color: var(--pal-bg-light);
    color: var(--pal-bg-dark);
    border: none;
    transition: all 250ms;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 10;
    cursor: pointer;
  }
  div.wrapper {
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 3rem;
    height: 3rem;
    border-radius: 50%;
    transition: all 250ms;
    z-index: 9;
  }
  div.wrapper:hover {
    transform: scale(150%, 150%);
  }
  div.backward {
    left: -1rem;
  }
  div.backward:hover {
    left: 0.2rem;
  }
  div.forward {
    right: calc(1vw + -1.5rem);
  }
  div.forward:hover {
    right: 0.2rem;
  }
</style>
