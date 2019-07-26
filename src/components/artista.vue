<template lang="pug">
  li.artista
    h2: a(:href="artista.url" target="_blank") {{ artista.name }}
    img(:src="artista.image[3]['#text']")
</template>

<script>
export default {
    name: 'artista',
    props: ['artista']
}
</script>

<style lang="stylus" scoped>
    li.artista  
        margin 10px 0
    img 
        margin 1px
        
  
</style>