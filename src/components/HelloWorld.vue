<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          src="https://upload.wikimedia.org/wikipedia/commons/d/df/TUIfly_737_01.jpg"
          class="my-3"
          contain
          height="400"
        />
      </v-col>

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          Hallo und<br>Willkommen zum Flugzeugquiz.<br> Lass uns starten!!!!
        </h1>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
        <h2 class="headline font-weight-bold mb-3">

        </h2>

        <v-row justify="center">
          <v-carousel
                  :show-arrows="false"
                  height="400"
                  hide-delimiters
                  v-model="q_index"
          >
            <v-carousel-item
                    v-for="(question, i) in questions"
                    :key="i"
            >
              <v-sheet
                      :color="question.color"
                      height="100%"
              >
                <v-row
                        class="fill-height"
                        align="center"
                        justify="center"
                >
                  <div class="display-3">{{question.q}}</div>
                  <v-btn rounded class="mx-2" @click="set_answer(0, question.correct)">{{question.answers[0]}}</v-btn>
                  <v-btn rounded class="mx-2" @click="set_answer(1, question.correct)">{{question.answers[1]}}</v-btn>
                  <v-btn rounded class="mx-2" @click="set_answer(2, question.correct)">{{question.answers[2]}}</v-btn>
                  <v-btn rounded class="mx-2" @click="set_answer(3, question.correct)">{{question.answers[3]}}</v-btn>
                </v-row>
              </v-sheet>
            </v-carousel-item>
          </v-carousel>
        </v-row>
      </v-col>
    </v-row>
    <v-snackbar
            v-model="snackbar"
            :timeout="0"
    >
      <p v-if="answer === correct">
        Das ist richtig!!!!
      </p>
      <p v-if="answer !== correct">
        Das war leider falsch.
      </p>
      <v-btn
              color="pink"
              text
              @click="next_q()"
      >
        Nächste Frage
      </v-btn>
    </v-snackbar>
  </v-container>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: () => ({
    set_answer(a, c) {
      this.answer = a;
      this.correct = c;
      this.snackbar = true;
    },
    next_q() {
      this.snackbar = false;
      this.q_index++;
    },
    snackbar: false,
    answer: undefined,
    correct: undefined,
    q_index: 0,
    questions: [
      {
        q: "Wer hat das Flugzeug erfunden?",
        answers: [
          "Leonardo Da Vinci",
          "Wright Brothers",
          "Michael Jackson",
          "Nikola Tesla",
        ],
        correct: 1,
        color:"blue darken-4"
      },
      {
        q: "Welches Passagier Flugzeug ist das größte der Welt?",
        answers: [
          "Cirrus SR22",
          "B747-400",
          "A380-800",
          "A350",
        ],
        correct: 2,
        color: "teal"
      },
      {
        q: "Welcher Flughafen ist der größte Flughafen der Welt?",
        answers: [
          "Doha International Airport",
          "Hartsfield Jackson International Airport",
          "Frankfurt Airport",
          "Berlin Tegel Airport",
        ],
        correct:1,
        color:"orange darken-4"
      },
    ]
  })
}
</script>
