<template>
    <button :class="mode">
        <slot></slot>
    </button>
</template>

<script>
export default {
    props: ['mode'],
}
</script>

<style scoped>
 
 button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #001d61;
  border: 1px solid #001d61;
  color: white;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #03319c;
  border-color:  #03319c;
}

.flat {
  background-color: transparent;
  color: #03319c;
  border: none;
}

.flat:hover,
.flat:active {
  background-color: #edd2ff;
}

</style>

