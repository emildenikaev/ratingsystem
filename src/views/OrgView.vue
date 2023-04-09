<template>
  <div class="about">
    <h1>{{ name }}</h1>
    <h2>ИНН: {{ inn }}</h2>
    <div class="icons">
      <div class="icons-wrap">
        <div>
          <img :src="yearsStatus" alt="money" class="icons-image" />
          <h4>Время на рынке: {{ yearsValue }}</h4>
        </div>
        <div>
          <img :src="capitalStatus" alt="money" class="icons-image" />
          <h4>Капитал: {{ capitalValues }}</h4>
        </div>
      </div>

      <div class="icons-wrap">
        <div>
          <img :src="contractsStatus" alt="money" class="icons-image" />
          <h4>Количество контрактов: {{ contractsValue }}</h4>
        </div>
        <div>
          <img
            :src="badlistStatus"
            alt="money"
            class="icons-image icons-image-last"
          />
          <h4>BlackList: {{ badlistValue }}</h4>
        </div>
      </div>
    </div>

    <h2>Рейтинг компании: {{ result }}</h2>
    <div>
      <h4>
        Основываясь на предоставленном рейтинге уровень доверия организации
        можно считать:
      </h4>
      <ul>
        <li>Высоким - больше 75 пунктов</li>
        <li>Средним - от 40 до 75 пунктов</li>
        <li>Низким - меньше 40 пунктов</li>
      </ul>
    </div>
    <h3>
      Формулу для оценки стабильности и надежности компании можно выразить
      следующим образом:
    </h3>

    <h4>
      Рейтинг = ((Годы работы * 0,3) + (Капитал * 0,3) + (Контракты * 0,3)) /
      3.6 * (Черный список * 0.5) * 100
    </h4>

    <p>
      Каждому критерию присваивается коэффициент 0,3, что указывает на то, что
      они одинаково важны при определении стабильности и надежности компании.
      Критерии оцениваются независимо по шкале от 1 до 4 (например, капитал
      более 10 млрд - 4, до 10 млрд, но больше 1млрд - 3, от 50 млн до 1млрд - 2
      и капитал меньше 50 млн - 1), за исключением наличия компании в черном
      списке, которое принимает значение от 1 до 2 (В нашем случае 2 -
      отсутствует в blacklist). Это связано с тем, что нахождение в черном
      списке может оказать значительное влияние на репутацию и надежность
      компании, что заслуживает большего внимания в этой формуле. Результат мы
      делим на 3,6 (максимальное значение) и умножаем на 100 для нормализации
      баллов.
    </p>
    <p>
      Эта формула работает, потому что она учитывает множество факторов, которые
      важны для определения стабильности и надежности компании. Количество лет
      работы является показателем опыта компании и ее способности противостоять
      колебаниям рынка. Капитал компании отражает ее финансовую устойчивость и
      способность инвестировать в свою деятельность. Количество заключенных
      контрактов является показателем успеха компании в заключении деловых
      сделок. Наконец, статус "черный список" указывает на любые красные флажки,
      о которых следует знать потенциальным инвесторам или партнерам.
    </p>
    <p>
      Объединив эти факторы в единый рейтинг, мы сможем легче сравнивать
      компании и оценивать их общую стабильность и надежность. Однако важно
      отметить, что эта формула не является исчерпывающей и должна
      использоваться в сочетании с другими исследованиями при оценке компании.
    </p>
    <hr />
  </div>
</template>

<style lang="scss">
.icons {
  margin-top: 50px;
  display: flex;
  &-image {
    border-radius: 50%;
    margin-right: 40px;
    margin-bottom: 20px;
    width: 230px;
    box-shadow: 0px 0px 10px 5px black;
  }
}

h4 {
  margin-right: 40px;
}

ul {
  list-style: none;
  border-left: 10px solid #78909c;
  padding: 0;
  font-family: "Lucida Sans";
  margin-left: 30px;
  li {
    padding: 10px;
  }
  li:nth-child(odd) {
    background: #e1f1ff;
  }
  li:nth-child(even) {
    background: white;
  }
}

@media (min-width: 1100px) {
  .icons-wrap {
    display: flex;
  }
}

@media (max-width: 900px) {
  .icons-wrap {
    margin-left: 40px;
  }
}
</style>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "org-info",
  computed: {
    name() {
      return this.$route.params.name;
    },
    inn() {
      return this.$route.params.inn;
    },
    badlistStatus() {
      return require(`../assets/badlist${this.$route.params.badlistStatus}.png`);
    },
    badlistValue() {
      return this.$route.params.badlistValue;
    },
    capitalStatus() {
      return require(`../assets/capital${this.$route.params.capitalStatus}.png`);
    },
    capitalValues() {
      return this.$route.params.capitalValues;
    },
    yearsStatus() {
      return require(`../assets/years${this.$route.params.yearsStatus}.png`);
    },
    yearsValue() {
      return this.$route.params.yearsValue;
    },
    contractsStatus() {
      return require(`../assets/contracts${this.$route.params.contractsStatus}.png`);
    },
    contractsValue() {
      return this.$route.params.contractsValue;
    },
    result() {
      return Math.round(
        ((+this.$route.params.badlistStatus * 0.3 +
          +this.$route.params.capitalStatus * 0.3 +
          +this.$route.params.contractsStatus * 0.3) /
          3.6) *
          (+this.$route.params.badlistStatus * 0.5) *
          100
      );
    },
  },
});
</script>
