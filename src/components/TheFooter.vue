<template>
    <footer>
        <p>
            Developed by 
             <a :href="github">Aimê Ramalho</a>
        </p>
        <p>Icons by 
            <a :href="icons8">Icons8</a>
        </p>
        <p>
            Background vector created by
            <a :href="freepik">3ab2ou</a>
        </p>
    </footer>
</template>

<script>
export default {
    name: 'Footer',
    data() {
        return {
            github: 'https://github.com/AimeAriadne',
            icons8: 'https://icons8.com/icon/EINqUt4JSfeM/adicionar',
            freepik: 'https://www.freepik.com/vectors/background'
        }
    }
}
</script>

<style scoped>

footer {
  background-color: white;
  color: #2c3e50;
  text-align: center;
  position:absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 3rem;
  display: flex;
  justify-content: space-evenly;
  align-items: center;

}

p {
    margin: 0;
}
a {
    text-decoration: none;
    color: rgb(46, 108, 150);
}

@media (max-width: 900px) {
  footer {
    flex-direction: column;
    height: 8rem;

  }
}
</style>
