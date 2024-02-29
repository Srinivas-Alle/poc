<script>
export default {
  data() {
    return {
      msg: "Hello World!",
      cards: [
      
      ],
    };
  },
  methods: {
    getColor(card) {
      if (card.status === "up") return "green";
      if (card.status === "reconnecting") return "grey";
      return "red";
    },
    async getLiveSatus() {
      const response = await fetch("https://mocki.io/v1/c489ccbb-3950-4909-ac44-aa69ce671d65");
        this.cards  = await response.json();
        console.log(response.json());
    },
  },
  mounted() {
    this.getLiveSatus();
    this.cards = [...this.cards, ...this.cards, ...this.cards];
  },
};
</script>

<template>
  <v-row>
    <v-col cols="12"> <span class="text-h4">Overview</span></v-col>
  </v-row>
  <v-row>
    <v-col v-for="card in cards" :key="card" cols="6" md="4">
      <v-card
        class="flex-1-0 ma-2 pa-2"
        :title="card.title"
        :subtitle="card.subTitle"
      >
        <v-chip :color="getColor(card)">
          {{ card.status }}
        </v-chip>
      </v-card>
    </v-col>
  </v-row>

  <!--  -->
</template>