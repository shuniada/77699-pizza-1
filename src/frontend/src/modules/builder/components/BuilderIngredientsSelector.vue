<template>
  <div class="content__ingridients">
    <div class="sheet">
      <h2 class="title title--small sheet__title">
        Выберите ингридиенты
      </h2>

      <div class="sheet__content ingridients">
        <div class="ingridients__sauce">
          <p>Основной соус:</p>
          <RadioButton
            v-for="sauce in Sauces"
            :key="sauce.id"
            label-class="radio ingridients__input"
            :checked="sauceId == sauce.id"
            name="sauce"
            :value="sauce.value"
            :item-desc="sauce.name"
            @change="changeSauce(sauce)"
          />
        </div>

        <div class="ingridients__filling">
          <p>Начинка:</p>

          <ul class="ingridients__list">
            <BuilderIngredientsItem
              v-for="filling in Ingredients"
              :key="filling.id"
              :filling="filling"
            />
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import RadioButton from "@/common/components/AppRadioButton";
import BuilderIngredientsItem from "@/modules/builder/components/BuilderIngredientsItem";
import { mapState } from "vuex";

export default {
  name: "BuilderIngredientsSelector",
  components: { RadioButton, BuilderIngredientsItem },
  data() {
    return {};
  },

  computed: {
    Ingredients() {
      return this.$store.state.Builder.Ingredients;
    },

    Sauces() {
      return this.$store.state.Builder.Sauces;
    },

    ...mapState("Builder", ["sauceId"]),
  },

  methods: {
    changeSauce(sauce) {
      this.$store.commit("Builder/CHANGE_SAUCE", {
        name: sauce.value,
        price: sauce.price,
        Id: sauce.id,
      });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/scss/blocks/ingridients.scss";
@import "~@/assets/scss/blocks/title.scss";
</style>
