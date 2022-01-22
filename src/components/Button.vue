<template>
    <button class="buttonContainer">
        <slot />
    </button>
</template>

<script>


export default {
  name: 'Button',
  components: {
    
  },
  props: [
  ]
}


</script>

<style scoped lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,100;1,200;1,300;1,400;1,500;1,600;1,700&display=swap');
@import "@/assets/colors.scss";

.buttonContainer {
    border: none;
    border-radius: 2px;
    padding: 8px 10px;
    font-size: 14px;
    cursor: pointer;
    background-color: $blue;
    outline: none;
    background-position: center;
    transition: background 220ms ease-in-out;
    color: $text;
    font-family: 'Montserrat', sans-serif;
    text-align: center;
    font-weight: 600;

    &:hover {
        background: #7076fa radial-gradient(circle, transparent 1%, #7076fa 1%) center/15000%;
    }

    &:active {
        background-color: #8287fa;
        background-size: 100%;
        transition: background 0s;
    }
}


</style>
