<template>
  <div class="block">
    <h1>Buttons</h1>
    <p>type | size | color</p>
  </div>
  <hr/>
  <div class="block">
    <p>button | big | green</p>
    <Button constructor="button" size="big" color="green">Button text</Button>
  </div>
  <div class="block">
    <p>button | medium | green</p>
    <Button constructor="button" size="medium" color="green">Button text</Button>
  </div>
  <div class="block">
    <p>link | small | red</p>
    <Button constructor="link" size="small" color="red">Button text</Button>
  </div>
  <div class="block">
    <p>button | medium | outline</p>
    <Button constructor="button" size="medium" color="outline">Button text</Button>
  </div>
  <div class="block">
    <p>basket | medium | red</p>
    <Button constructor="basket" size="medium" color="red">
      <template v-slot:number>5</template>
      <template v-slot:content>Basket</template>
    </Button>
  </div>
  <div class="block">
    <p>basket +1 | medium | green</p>
    <Button constructor="btnPlusOne" size="medium" color="green">
      <template v-slot:content>Button Plus One</template>
    </Button>
  </div>
  <div class="block">
    <p>basket [-1+] | medium | green</p>
    <Button constructor="btnCount" size="medium" color="green">
      <template v-slot:content>Button Count</template>
    </Button>
  </div>
</template>

<script>
import Button from "./components/Button.vue";

export default {
  name: "App",
  components: {
    Button: Button,
  },
  data() {
    return {
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  padding: 0;
  margin: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
  margin-bottom: 40px;
}

h1 {
  padding-bottom: 0;
  margin: 0;
}

a {
  color: #3FB983;
  text-decoration: none;
}

a:hover {
  color: #FF5C6A;
  text-decoration: underline;
}

.block {
  padding-bottom: 2rem;
}

hr {
  border: none;
  display: block;
  height: 1px;
  background-color: #eee;
  margin-top: 0;
  margin-bottom: 3rem;
}
</style>
