<template>
    <CatImage/>
</template>

<script>
// Import the file CatImage
import CatImage from '../components/CatImage.vue';

export default {
    name: "home",
    components: {
        CatImage,
    }
}

</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Dosis:wght@200;300;400;500;600;700&display=swap');

/* color: #56B7A7 */
body{
    background-color: #FFFFFF;
    font-family: 'Dosis', sans-serif;
}
@media screen and (max-width: 640px) {
  body{
    background-color: #529b7734;
    font-family: 'Dosis', sans-serif;
}
}
</style>
