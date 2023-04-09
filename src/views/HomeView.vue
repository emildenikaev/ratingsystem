<template>
  <div class="home">
    <div class="container">
      <img src="../assets/rating.jpeg" alt="Информация" class="image" />
      <div>
        <p>
          Проверьте надежность вашего контрагента, введите его ИНН в нашем
          бесплатном сервисе:
        </p>
        <div class="text-field">
          <div class="text-field__group">
            <input
              v-model="innform"
              class="text-field__input"
              type="search"
              id="search"
              name="search"
              placeholder="Введите ИНН"
            />
            <button
              class="text-field__btn btn"
              type="button"
              @click="sendRequest"
            >
              ПРОВЕРИТЬ
            </button>
          </div>
        </div>
        <p v-if="showFlash" class="flash">Введите корректный ИНН</p>
      </div>
    </div>
    <HelloWorld />
  </div>
</template>

<script>
import { defineComponent } from "vue";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src

import axios from "axios";

export default defineComponent({
  name: "HomeView",
  components: {
    HelloWorld,
  },
  data() {
    return {
      innform: "",
      showFlash: false,
    };
  },
  methods: {
    async sendRequest() {
      try {
        const response = await axios.post("http://46.243.227.152:8000/data", {
          user_form: {
            innform: this.innform,
          },
        });
        if (response.data.found) {
          this.$router.push({
            name: "org-info",
            params: {
              inn: response.data.inn,
              name: response.data.name,
              badlistStatus: response.data.badlist.status,
              badlistValue: response.data.badlist.value,
              capitalStatus: response.data.capital.status,
              capitalValues: response.data.capital.values,
              yearsStatus: response.data.years.status,
              yearsValue: response.data.years.value,
              contractsStatus: response.data.contracts.status,
              contractsValue: response.data.contracts.value,
            },
          });
        } else {
          this.showFlash = true;
        }
        console.log(response.data);
      } catch (error) {
        console.error(error);
      }
    },
  },
});
</script>

<style lang="scss">
.container {
  display: flex;
  align-items: center;
  max-width: 1100px;
  margin: 0 auto;
  .image {
    margin-right: 30px;
  }
}

.container .btn {
  background-color: #6eb4fa;
  color: white;
  font-size: 16px;
  padding: 20px 40px;
  border: none;
  cursor: pointer;
  border-radius: 10px;
}

.container .main {
  color: #202020;
  text-shadow: 1px 1px 0 #6eb4fa;
}

.container .btn:hover {
  color: #cecece;
}

.text-field__group {
  display: flex;
  justify-content: center;
}
.text-field__btn {
  display: inline-block;
  font-weight: 400;
  line-height: 1.5;
  color: #212529;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  user-select: none;
  background-color: #cecece;
  border: 1px solid #6eb4fa;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  border-radius: 0.25rem;
  transition: background-color 0.15s ease-in-out;
}
.text-field__btn:hover {
  color: #cecece;
}
.text-field__group .text-field__input {
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
  position: relative;
  z-index: 2;
  border: 2px solid #6eb4fa;
  border-radius: 10px 0 0 10px;
}

input:focus {
  outline: none;
}

.text-field__group .text-field__btn {
  position: relative;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
  border-left-width: 0;
}
input {
  padding-left: 28px;
  padding-right: 5px;
}

input[type="search"]::-webkit-search-decoration,
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-results-button,
input[type="search"]::-webkit-search-results-decoration {
  display: none;
}

.flash {
  color: #d61515;
}

@media (max-width: 1100px) {
  .container .main {
    top: 20%;
    font-size: 16px;
  }
  .container {
    display: flex;
    flex-direction: column;
  }
  .container .main {
    display: none;
  }
}
</style>
