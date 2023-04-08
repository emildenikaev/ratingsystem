<template>
  <div class="home">
    <div class="container">
      <img
        src="../assets/rating.jpeg"
        alt="Информация"
        class="py-7 py-md-0 bg-hero image"
      />
      <router-link to="/analytics">
        <button class="btn">Аналитика</button>
      </router-link>
    </div>
    <HelloWorld />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src

export default defineComponent({
  name: "HomeView",
  components: {
    HelloWorld,
  },
});
</script>

<style lang="scss">
.image {
  width: 100vw;
  box-sizing: border-box;
  overflow: hidden;
}

.container {
  position: relative;
  width: 50vw;
}

/* Make the image responsive */
.container img {
  width: 100vw;
  height: auto;
}

/* Style the button and place it in the middle of the container/image */
.container .btn {
  position: absolute;
  top: 60%;
  left: 50vw;
  transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  background-color: #6eb4fa;
  color: white;
  font-size: 16px;
  padding: 20px 40px;
  border: none;
  cursor: pointer;
  border-radius: 10px;
}

.container .main {
  position: absolute;
  top: 40%;
  width: 100%;
  left: 50vw;
  transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  color: #202020;
  text-shadow: 1px 1px 0 #6eb4fa;
}

.container .btn:hover {
  color: #cecece;
}

@media (max-width: 1100px) {
  .container .main {
    top: 20%;
    font-size: 16px;
  }
}

@media (max-width: 567px) {
  .container .main {
    display: none;
  }
}
</style>
