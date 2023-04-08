<template>
  <div>
    <nav>
      <div class="header header-first">
        <a class="logo">RUSFUTURE</a>
        <div class="info">
          <a class="slogan">ОЦЕНИТЕ СВОИ УСПЕХИ </a>
          <a class="slogan-second">С ПОМОЩЬЮ РЕЙТИНГА</a>
        </div>
      </div>
      <div class="header">
        <router-link to="/" class="header-main">Главная</router-link>
        <router-link to="/analytics">Аналитика</router-link>
      </div>
    </nav>
    <router-view />
    <nav class="footer">
      <p>© 2023 RUSFUTURE - All Rights Reserved</p>
    </nav>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  font: 16px/22px Roboto, sans-serif;
  color: #202020;
  background-color: #fbfbfb;
}

.header {
  display: flex;
  align-items: center;
  margin-right: 40px;
  margin-left: 40px;
  &-main {
    margin-right: 40px;
  }
}

nav {
  padding: 30px;
  width: 100vw;
  display: flex;
  justify-content: space-between;
  align-items: center;
  :hover {
    color: #cecece;
  }
  a {
    font-weight: bold;
    color: #202020;
    &.router-link-exact-active {
      color: #6eb4fa;
    }
  }
  a.logo {
    color: #202020;
    margin-right: 40px;
    :hover {
      color: #cecece;
    }
  }
  .info {
    display: flex;
    flex-direction: column;
    a.slogan {
      color: #6eb4fa;
      &-second {
        color: white;
        background: #6eb4fa;
        border-radius: 5px;
        padding: 4px;
      }
    }
  }
}
nav.footer {
  display: flex;
  justify-content: space-around;
}
@media (max-width: 585px) {
  .header-first {
    display: none;
  }
}
</style>
