<template>
   <div>
      <h3>{{ obj.cod }}</h3>
      <h2>{{ obj.message }} &#128532;</h2>
   </div>
</template>

<script>
export default {
   props: ['obj'],
};
</script>

<style lang="scss" scoped>
div {
   background-color: #141313;
   width: 400px;
   margin: auto;
   border-radius: 0 0 15px 15px;
   color: crimson;
   padding: 15px;
   box-shadow: 0 0 5px red;
   font-size: 2rem;
   position: relative;
   bottom: 12px;
}
</style>
