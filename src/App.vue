<template>
  
  <p class="loading" v-if="loading">Loading...</p>

  <main v-else>

    <section v-if="state.currentQuestion < state.questions.length" >
      
      <div class="question">
        <h2 v-html="state.questions[state.currentQuestion].question"></h2>
      </div>
      
      <div class="answers">
        <div
          v-for="answer in state.questions[state.currentQuestion].answers"
          :key="answer"
          @click="checkAnswer(answer)" 
          class="answer"
        >
          <span v-html="answer"></span>
        </div>
      </div>

      <div class="score">
        <h3>Score: {{score + '/' + totalAttempted}}</h3>
      </div>

    </section>

    <section v-else class="done">
      <div class="final-score">Your Score: {{ score + '/' + totalScore }} </div>
      <button @click="playAgain()" class="btn-again">Play Again</button>
    </section>

  </main>


</template>

<script setup>
// import ref, reactive, computed and onMounted from vue

// define state with reactive() and loading with ref()

// define computed properties


// The Fetch Questions function - don't change
const fetchQuestions = async (amount) => {
let {results} = await (await fetch(`https://opentdb.com/api.php?amount=${amount}&category=18&difficulty=easy&type=multiple`)).json()
let questions = results.map((question) => {
    let answers = [...question.incorrect_answers, question.correct_answer];
    return {
      ...question,
      answers: answers.sort(() => Math.random() - 0.5),
    };
  });
    return questions;
};


const checkAnswer = (answer) => {
  // check if answer is correct -> increment correctAnswers and currentQuestion
};


const playAgain = async () => {
  // reset state
  // fetch new questions
};

// use onMounted() to fetch questions


</script>
