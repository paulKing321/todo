<template>
  <div class="about">
    <h1>This is a simple todo app to keep you up and running</h1>
    <h2>You are Welcome</h2>
    
    <div class="img">
      <img src="../images/paul.jpg">
    </div>
    <footer>Made with love by PaulKing</footer>
  </div>
</template>

<style scoped>
.about {
  text-align: center;
  align-items: center;
  justify-content: center;
  justify-items: center;
  margin: 0 auto;
}
.img img {
  width: 25%;
  border-radius: 50%;
  margin-top: 30px;
  border: 4px #fd068e solid;
}
footer {
  font-weight: bolder;
  margin-top: 10px;
  /* position: absolute; */
  text-shadow: 0 0 0.125em hsl(0 0% 100% / 0.3), 0 0 0.45em currentColor;

}
.about h2 {
  color: #fd068e;
    text-shadow: 0 0 0.125em hsl(0 0% 100% / 0.3), 0 0 0.45em white;

}
</style>