<script context="module" lang="ts">
  let onTop; //keeping track of which open modal is on top
  const modals = {}; //all modals get registered here for easy future access

  // 	returns an object for the modal specified by `id`, which contains the API functions (`open` and `close` )
  export function getModal(id = "") {
    return modals[id];
  }
</script>

<script lang="ts">
  import { onDestroy } from "svelte";

  let topDiv;
  let visible = false;
  let prevOnTop;

  export let id = "";

  function keyPress(ev) {
    if (ev.key == "Escape" && onTop == topDiv) close();
  }

  function open() {
    if (visible) return;
    window.addEventListener("keydown", keyPress);
    prevOnTop = onTop;
    onTop = topDiv;
    document.body.style.overflow = "hidden";
    visible = true;
    document.body.appendChild(topDiv);
  }

  function close() {
    if (!visible) return;
    window.removeEventListener("keydown", keyPress);
    onTop = prevOnTop;
    if (onTop == null) document.body.style.overflow = "";
    visible = false;
  }

  //expose the API
  modals[id] = { open, close };

  onDestroy(() => {
    delete modals[id];
    window.removeEventListener("keydown", keyPress);
  });
</script>

<div id="topModal" class:visible bind:this={topDiv} on:click={() => close()}>
  <div id="modal" on:click|stopPropagation={() => {}}>
    <svg id="close" on:click={() => close()} viewBox="0 0 12 12">
      <circle cx="6" cy="6" r="6" />
      <line x1="3" y1="3" x2="9" y2="9" />
      <line x1="9" y1="3" x2="3" y2="9" />
    </svg>
    <div id="modal-content">
      <slot />
    </div>
  </div>
</div>

<style>
  #topModal {
    visibility: hidden;
    z-index: 9999;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(31, 31, 31, 0.805);
    display: flex;
    align-items: center;
    justify-content: center;
  }

  #modal {
    position: relative;
    border-radius: 6px;
    background: white;
    border: 1px solid #000;
    padding: 2em;
  }

  .visible {
    visibility: visible !important;
  }

  #close {
    position: absolute;
    top: -8px;
    right: -8px;
    width: 24px;
    height: 24px;
    fill: rgb(217, 43, 43);
    transition: transform 0.2s;
  }

  #close:hover {
    transform: scale(1.5);
  }

  #close line {
    stroke: rgb(255, 255, 255);
    stroke-width: 1.5;
  }
</style>
