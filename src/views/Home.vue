<template>
  <header class="theme">
    <img
      src="https://awrestaurants.com/sites/default/files/Spicy%20Papa%20Burger%20Combo%20Web%20Header_0.jpg"
    />
    <h1>Welcome to BurgerOnline</h1>
  </header>
  <section class="burgerinfo">
    <h2>Select burger</h2>
    <p>Here you can select the burger you want</p>
    <div class="wrapper">
      <Burger
        class="burgerBoxes"
        v-for="burger in burgers"
        v-bind:burger="burger"
        v-bind:key="burger.name"
        v-on:orderedBurger="addToOrder($event)"
      />
      {{ amountOrdered }}
      <!-- följde med från början
      <div id="map" v-on:click="addOrder">click here</div>
      -->
      <!-- Gammal display av burgare
      <div class="box a" style="float: left">
        <h3>The shoe burger</h3>
        <img
          src="https://cdn.trendhunterstatic.com/phpthumbnails/22/22829/22829_1_800.jpeg"
          style="height: 200px; width: 200px"
        />
        <ul>
          <li>Not wearable</li>
          <li>Not a real shoe</li>
          <li><span id="ingredient">Gluten</span> free</li>
        </ul>
      </div>
      <div class="box b" style="float: left">
        <h3>The cute burgerino</h3>
        <img
          src="https://rlv.zcache.se/cute_buns_funny_burger_pun_poster-r7d0ec32519e5481bbb68fa2dceaf02ac_w2q_8byvr_307.jpg"
          style="height: 200px; width: 200px"
        />
        <ul>
          <li>Can bite though</li>
          <li>Very tasty</li>
          <li><span id="ingredient">Gluten</span> neutral</li>
        </ul>
      </div>
      -->
    </div>
  </section>
  <section style="clear: both" id="orderform">
    <h2>Provide information</h2>
    <p>
      Here you will provide the information so that we can send the burger to
      you
    </p>
    <form>
      <h3>Delivery information:</h3>
      <p>
        <label for="fullname">Full name</label>
        <br />
        <!--
        <input
          type="text"
          id="fullname"
          name="fn"
          required="required"
          placeholder="First- and Last name"
        />
        -->
        <input v-model="fullName" placeholder="Full Name" />
        The name: {{ fullName }}
      </p>
      <p>
        <label for="email">E-mail</label>
        <br />
        <!--
        <input
          type="email"
          id="email"
          name="em"
          required="required"
          placeholder="E-mail address"
        /> -->
        <input v-model="eMail" placeholder="E-mail adress" />
      </p>
      <!--
      <p>
        <label for="street">Street</label>
        <br />
        <input
          type="text"
          id="street"
          name="st"
          required="required"
          placeholder="Street name"
        />
        
        <input v-model="street" placeholder="Street name" />
      </p>
      <p>
        <label for="fullname">House</label>
        <br />
        
        <input
          type="number"
          id="house"
          name="hs"
          required="required"
          placeholder="House number"
        />
        <input v-model="houseNumber" placeholder="House number" />
      </p>-->
      <p>
        <label for="payment">Payment options</label>
        <br />
      </p>
      <div id="v-model-select" class="selectpayment">
        <select v-model="recipient">
          <option diables value="">Please select one</option>
          <option>Sweden HQ</option>
          <option>London HQ</option>
          <option>PayPal</option>
          <option>Cash</option>
          <option>BitCoin</option>
        </select>
      </div>
      <p>
        <label for="gender">Select gender</label>
        <br />
      </p>

      <div id="v-model-radiobutton">
        <input type="radio" id="male" value="Male" v-model="gender" />
        <label for="male"> Male </label>
        <input type="radio" id="female" value="Female" v-model="gender" />
        <label for="female"> Female </label>
        <input type="radio" id="undefined" value="Undefined" v-model="gender" />
        <label for="undefined"> Undefined </label>
      </div>
      <br />
      <label for="mapcontainer"> Please choose location: </label>
      <div id="mapcontainer">
        <div id="map" v-on:click="setLocation">
          <div
            v-bind:style="{ left: location.x + 'px', top: location.y + 'px' }"
          >
            T
          </div>
        </div>
      </div>
    </form>
    <p>
      Alla värden:
      <br />
      {{ fullName }}
      <br />
      {{ eMail }}
      <br />
      {{ street }}
      <br />
      {{ houseNumber }}
      <br />
      {{ recipient }}
      <br />
      {{ gender }}
      <br />
      {{ orderedBurger }}
    </p>
  </section>
  <div id="order">
    <button v-on:click="orderButton" type="submit">
      <img
        src="https://i.pinimg.com/474x/3d/fb/6a/3dfb6acb0b823e78eff8ab8c14ab706f.jpg"
        style="width: 25px"
      />
      Order
    </button>
  </div>
  <hr />

  <footer>&copy;</footer>
</template>

<script>
import Burger from "../components/Burger.vue";
import io from "socket.io-client";
import menu from "../assets/menu.json";

const socket = io();

/*class MenuItem {
  constructor(productName, imageURL, kCal, gluten, lactose) {
    this.name = productName;
    this.imageURL = imageURL;
    this.kCal = kCal;
    this.gluten = gluten;
    this.lactose = lactose;
  }
}

let burgers = [
  new MenuItem(
    "Birger",
    "https://assets.icanet.se/e_sharpen:80,q_auto,dpr_1.25,w_718,h_718,c_lfill/imagevaultfiles/id_226596/cf_259/smash_burger_fran_oklahoma.jpg",
    "600",
    true,
    false
  ),
  new MenuItem(
    "Birger",
    "https://assets.icanet.se/e_sharpen:80,q_auto,dpr_1.25,w_718,h_718,c_lfill/imagevaultfiles/id_226596/cf_259/smash_burger_fran_oklahoma.jpg",
    "600",
    true,
    true
  ),
];
console.log(burgers);
*/

export default {
  name: "Home",
  components: {
    Burger,
  },
  data: function () {
    return {
      burgers: menu,
      fullName: "",
      eMail: "",
      recipient: "",
      gender: "",
      orderedBurger: {},
      location: { x: 0, y: 0 },
    };
  },
  methods: {
    orderButton: function () {
      console.log(
        this.fullName,
        this.eMail,
        this.gender,
        this.recipient,
        this.location
      );
      socket.emit("addOrder", {
        orderId: this.getOrderNumber(),
        details: this.location,
        fullName: this.fullName,
        eMail: this.eMail,
        recipient: this.recipient,
        gender: this.gender,
        orderItems: this.orderedBurger,
      });
    },
    addToOrder: function (event) {
      this.orderedBurger[event.name] = event.amount;
      console.log(this.orderedBurger.Normal);
    },
    getOrderNumber: function () {
      return Math.floor(Math.random() * 100000);
    },
    setLocation: function (event) {
      var offset = {
        x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top,
      };
      //Stores location
      this.location = {
        x: event.clientX - 10 - offset.x,
        y: event.clientY - 10 - offset.y,
      };
    },
    addOrder: function (event) {
      var offset = {
        x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top,
      };
      socket.emit("addOrder", {
        orderId: this.getOrderNumber(),
        details: {
          x: event.clientX - 10 - offset.x,
          y: event.clientY - 10 - offset.y,
        },
        orderItems: ["Beans", "Curry"],
      });
    },
  },
};
</script>

<style>
#map {
  height: 1070px;
  width: 1920px;

  position: relative;
  margin: 0;
  padding: 0;
  background: url(/img/polacks.jpg);
  background-repeat: no-repeat;
  width: 1920px;
  height: 1078px;
  cursor: crosshair;
  /*background-color: red;*/
  background: url("/img/polacks.jpg");
}

#mapcontainer {
  width: 30em;
  height: 15em;
  overflow: scroll;
}

#map div {
  position: absolute;
  background: black;
  color: white;
  border-radius: 10px;
  width: 20px;
  height: 20px;
  text-align: center;
}

/*empty*/
body {
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  font-size: 19px;
}

.theme {
  margin: 20px;
  padding: 20px;
}

header {
  margin: 0px 20px;
  padding: 2px;
}

header,
header img {
  height: 200px;
  overflow: hidden;
}

header h1 {
  position: absolute;
  left: 130px;
  top: 30px;
}
header img {
  opacity: 0.4;
  width: 100%;
  height: auto;
}

section {
  margin: 0.5em 20px;
  padding: 0px 15px;
}

.wrapper {
  display: grid;
  grid-gap: 10px;
  grid-template-columns: 33% 33% 33%;
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

/*section > div {
  padding: 10px;
}*/

button {
  margin: 20px;
}

button:hover {
  background-color: blue;
  cursor: pointer;
}

.burgerinfo {
  background-color: black;
  color: white;
  float: left;
  border: 2px dashed white;
  width: 670px;
}

#orderform {
  border: 2px dashed black;
  width: 670px;
}

.ingredient {
  font-weight: bold;
}
</style>
