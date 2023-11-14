<template>
  <nav class="button-container">
    <button type="button" class="custom-button" @click="undo">
      <svg width="42" height="38" viewBox="0 0 42 38" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect width="42" height="38" rx="4" fill="#282828" />
        <path d="M28.6358 29.5824C28.3582 29.86 27.9929 30 27.6299 30C27.2645 30 26.8992 29.86 26.6216 29.5824C26.0664 29.0249 26.0664 28.1257 26.6216 27.5682C29.7604 24.4294 29.7604 19.3238 26.6216 16.1851C23.4852 13.0486 18.3772 13.0486 15.2408 16.1851L14.726 16.6999H18.1234C18.9087 16.6999 19.5469 17.3381 19.5469 18.1234C19.5469 18.911 18.9087 19.5469 18.1234 19.5469H11.4235C10.6382 19.5469 10 18.911 10 18.1234V11.4235C10 10.6382 10.6382 10 11.4235 10C12.2088 10 12.847 10.6382 12.847 11.4235V14.5528L13.2266 14.1732C17.4757 9.92408 24.3867 9.92408 28.6358 14.1732C32.8849 18.4223 32.8849 25.3333 28.6358 29.5824Z" fill="#639EFF" />
      </svg>
    </button>
    <button type="button" class="custom-button" @click="redo">
      <svg width="42" height="38" viewBox="0 0 42 38" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect width="42" height="38" rx="4" fill="#282828" />
        <path d="M13.1868 29.5824C13.4644 29.86 13.8298 30 14.1928 30C14.5581 30 14.9235 29.86 15.2011 29.5824C15.7562 29.0249 15.7562 28.1257 15.2011 27.5682C12.0623 24.4294 12.0623 19.3238 15.2011 16.1851C18.3375 13.0486 23.4454 13.0486 26.5819 16.1851L27.0967 16.6999H23.6993C22.914 16.6999 22.2758 17.3381 22.2758 18.1234C22.2758 18.911 22.914 19.5469 23.6993 19.5469H30.3992C31.1845 19.5469 31.8227 18.911 31.8227 18.1234V11.4235C31.8227 10.6382 31.1845 10 30.3992 10C29.6139 10 28.9757 10.6382 28.9757 11.4235V14.5528L28.5961 14.1732C24.347 9.92408 17.4359 9.92408 13.1868 14.1732C8.93773 18.4223 8.93773 25.3333 13.1868 29.5824Z" fill="#639EFF" />
      </svg>
    </button>
    <button type="button" class="custom-button" @click="convertElementsToHeading">
      <svg width="42" height="38" viewBox="0 0 42 38" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect width="42" height="38" rx="4" fill="#282828" />
        <path d="M31 9.5V12.0075C31 12.8375 30.3317 13.5075 29.5037 13.5075C28.6783 13.5075 28.0075 12.8375 28.0075 12.0075V11H22.4963V28H23.8454C24.6733 28 25.3416 28.6725 25.3416 29.5C25.3416 30.3275 24.6733 31 23.8454 31H18.1546C17.3267 31 16.6584 30.3275 16.6584 29.5C16.6584 28.6725 17.3267 28 18.1546 28H19.5037V11H13.9925V12.0075C13.9925 12.8375 13.3217 13.5075 12.4963 13.5075C11.6683 13.5075 11 12.8375 11 12.0075V9.5C11 8.6725 11.6683 8 12.4963 8H29.5037C30.3317 8 31 8.6725 31 9.5Z" fill="#639EFF" />
      </svg>
    </button>
    <button type="button" class="custom-button" @click="convertElementsToParagraph">
      <svg width="42" height="38" viewBox="0 0 42 38" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect width="42" height="38" rx="4" fill="#282828" />
        <path d="M20.4876 14.7416V16.0604C20.4876 16.9872 19.7344 17.7404 18.8076 17.7404C18.004 17.7404 17.332 17.1748 17.1668 16.4216H16.0048V23.5868C16.8476 23.6792 17.5056 24.3932 17.5056 25.2584C17.5056 26.188 16.7524 26.9384 15.8256 26.9384H12.824C11.8944 26.9384 11.144 26.188 11.144 25.2584C11.144 24.3932 11.7992 23.6792 12.6448 23.5868V16.4216H11.48C11.3148 17.1748 10.6428 17.7404 9.8392 17.7404C8.9124 17.7404 8.15919 16.9872 8.15919 16.0604V14.7416C8.15919 13.812 8.9124 13.0616 9.8392 13.0616H18.8076C19.7344 13.0616 20.4876 13.812 20.4876 14.7416Z" fill="#639EFF" />
        <path d="M33.9192 14.7416V16.0604C33.9192 16.9872 33.1688 17.7404 32.2392 17.7404C31.4356 17.7404 30.7636 17.1748 30.5984 16.4216H29.4364V23.5868C30.2792 23.6792 30.9372 24.3932 30.9372 25.2584C30.9372 26.188 30.184 26.9384 29.2572 26.9384H26.2556C25.326 26.9384 24.5756 26.188 24.5756 25.2584C24.5756 24.3932 25.2308 23.6792 26.0764 23.5868V16.4216H24.9144C24.7492 17.1748 24.0772 17.7404 23.2708 17.7404C22.344 17.7404 21.5908 16.9872 21.5908 16.0604V14.7416C21.5908 13.812 22.344 13.0616 23.2708 13.0616H32.2392C33.1688 13.0616 33.9192 13.812 33.9192 14.7416Z" fill="#639EFF" />
      </svg>
    </button>
    <button type="button" class="custom-button" @click="insertImage">
      <svg width="42" height="38" viewBox="0 0 42 38" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect x="4.57764e-05" width="42" height="38" rx="4" fill="#282828" />
        <path d="M30.5652 9.07849H11.4348C10.6433 9.07849 10 9.72175 10 10.5133V27.4868C10 28.2783 10.6433 28.9215 11.4348 28.9215H30.5652C31.3567 28.9215 32 28.2783 32 27.4868V10.5133C32 9.72175 31.3567 9.07849 30.5652 9.07849ZM29.1304 26.052H12.8696V25.3274L15.9496 22.2474L17.3867 23.6822C17.9463 24.2441 18.855 24.2441 19.4146 23.6846L25.0843 18.0148L29.1304 22.0609V26.052ZM29.1304 18.0052L26.0983 14.9707C25.5363 14.4111 24.63 14.4111 24.068 14.9707L18.4007 20.6404L16.9635 19.2033C16.4039 18.6437 15.4952 18.6437 14.9357 19.2033L12.8696 21.2694V11.9481H29.1304V18.0052Z" fill="#639EFF" />
        <path d="M17.7591 17.2558C16.765 17.2558 15.9563 16.447 15.9563 15.453C15.9563 14.4589 16.765 13.6502 17.7591 13.6502C18.7531 13.6502 19.5619 14.4589 19.5619 15.453C19.5619 16.447 18.7531 17.2558 17.7591 17.2558Z" fill="#639EFF" />
      </svg>
    </button>
    <button type="button" class="custom-button" @click="copyHTML">
      Скопировать HTML
    </button>
  </nav>
</template>

<script setup>
const emit = defineEmits(['undo', 'redo', 'convert-elements-to-tag', 'insert-image', 'copy-html']);

function undo() {
  emit('undo')
}

function redo() {
  emit('redo')
}

function convertElementsToHeading() {
  emit('convert-elements-to-tag', 'h2')
}

function convertElementsToParagraph() {
  emit('convert-elements-to-tag', 'p')
}

function insertImage() {
  emit('insert-image')
}

function copyHTML() {
  emit('copy-html')
}
</script>

<style>
.button-container {
  display: flex;
  align-items: center;
  padding-bottom: clamp( .2rem, 3.229vw, 1.938rem);
}

.custom-button {
  border: none;
  display: inline-flex;
  margin-right: clamp( .25rem, 1.25vw, .75rem);
  font-size: clamp( .5rem, 1.3542vw, .8125rem);
  padding: 0;
  border-radius: 4px;
  cursor: pointer;
  color: var(--color-button);
  background-color: transparent;
  transition: all 0.2s ease;
}

.custom-button svg path{
  transition: all 0.2s ease;
}

.custom-button:hover svg path,
.custom-button:hover {
  fill: var(--color-button-hover);
  color: var(--color-button-hover);
}
</style>
