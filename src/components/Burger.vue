<template>
  <div class="burgers">
    <h3 v-bind:key="burger.name">
      {{ burger.name }}
    </h3>
    <img v-bind:src="burger.imageURL" style="width: 200px" />
    <h4>Contents:</h4>
    <ul>
      <li>{{ burger.kCal }} kCal</li>
      <li v-if="burger.gluten">
        Contains <span class="warningIngredient"> gluten </span>
      </li>
      <li v-if="burger.lactose">
        Contains <span class="warningIngredient"> lactose </span>
      </li>
    </ul>
    <button v-on:click="increaseAmountOrdered">+</button>
    {{ amountOrdered }}
    <button v-on:click="decreaseAmountOrdered">-</button>
    <!--
      <img
      src="https://media-cdn.tripadvisor.com/media/photo-s/08/04/2d/c4/funny-burger.jpg"
      style="height: 200px; width: 200px"
    /> 
    <ul>
      <li>Very big</li>
      <li>Enormous</li>
      <li><span id="ingredient">Gluten</span> full</li>
    </ul>
    -->
  </div>
</template>

<script>
export default {
  name: "Burger",
  img: "",
  props: {
    burger: Object,
  },
  data: function () {
    return {
      amountOrdered: 0,
    };
  },
  methods: {
    increaseAmountOrdered: function () {
      this.amountOrdered++;
      this.$emit("orderedBurger", {
        name: this.burger.name,
        amount: this.amountOrdered,
      });
    },
    decreaseAmountOrdered: function () {
      if (this.amountOrdered > 0) {
        this.amountOrdered--;
      }
      this.$emit("orderedBurger", {
        name: this.burger.name,
        amount: this.amountOrdered,
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  font-size: 19px;
}

.warningIngredient {
  font-weight: bold;
}

.wrapper {
  display: grid;
  grid-gap: 10px;
}
.a {
  grid-column: 1;
}
.b {
  grid-column: 2;
}
.c {
  grid-column: 3;
}

.burgerinfo {
  background-color: black;
  color: white;
  float: left;
  border: 2px dashed white;
  width: 670px;
}
</style>
