<template>
  <div class="home">
    <p>Your Meal Suggestion:</p>
    <h1>{{ currentSuggestion || "I'm outta ideas" }}</h1>
    <button @click="suggest(slop)">SLOP</button>
    <button @click="suggest(notSlop)">NOT SLOP</button>
    <button @click="suggest(eatOut)">EAT OUT</button>
    <button @click="suggest(carbs)">CARBS</button>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  components: {},
  data() {
    return {
      currentSuggestion: null,
      slop: new Shuffler([
        "Golumpkis",
        "Pasta & Beef Sauce",
        "Beef Cauliflower Rice",
      ]),
      notSlop: new Shuffler(["Pork", "Steak"]),
      eatOut: new Shuffler(["Plaza Azteca", "Chik Fil A", "Sophias"]),
      carbs: new Shuffler(["Grilled Cheese & Soup", "Nachos"]),
    };
  },
  methods: {
    suggest(category) {
      this.currentSuggestion = category.drawNext();
    },
  },
};

class Shuffler {
  constructor(array) {
    this.elements = [...array];
    let remainingElements = this.elements.length,
      elementToSwap,
      nextElementIndex;

    while (remainingElements > 0) {
      nextElementIndex = Math.floor(Math.random() * remainingElements--);
      elementToSwap = this.elements[remainingElements];
      this.elements[remainingElements] = this.elements[nextElementIndex];
      this.elements[nextElementIndex] = elementToSwap;
    }
  }

  drawNext() {
    return this.elements.pop();
  }
}
</script>
