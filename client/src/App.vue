<template>
<div id="app">
  <div class="header">
    <div class="title">
      <h1>Fantasy Character Maker</h1>
    </div>
  </div>
  <div class="content">
    <router-view />
  </div>
  <div class="footer">
    <router-link to="/">Home</router-link> <br/>
    <router-link to="/CharacterCreator">Create a Character</router-link>
    <footer>Login</footer>
    <footer><a href="https://github.com/diaxenl/260-final-project.git">GitHub</a></footer>
  </div>
</div>
</template>

<style>
html {
  box-sizing: border-box;
}

body {
  display: grid;
  font-family: 'Montserrat', sans-serif;
  font-size: 16px;
  background: #fff;
  padding: 0px;
  margin: 0px;
}

/* Header */
.header {
  display: flex;
  justify-content: center;
  background-image: url('https://previews.123rf.com/images/flukesamed/flukesamed1404/flukesamed140400026/27372625-blaze-fire-flame-for-banner-background.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  padding: 10px 100px 0px 100px;
  color: #1C454F;
}

.title {
  margin-top: 5px;
}

.title h1 {
  font-size: 30px;
}

.content {
  padding: 20px 100px;
  min-height: 500px;
}

/* Footer */
.footer {
  height: 50px;
  padding: 20px 100px 0px 100px;
  background: #e3e3e3;
  font-size: 12px;
}

.footer a {
  color: #000;
}

h1 {
  font-size: 20px;
}

h2 {
  font-size: 14px;
}
</style>