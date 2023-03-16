<template>
    

  <div class="quiz">
    <h1 class="quiz__title">{{ quizData.title }}</h1>

    <div v-if="!quizCompleted" class="quiz__question">
      <h2 class="question__number">
        Question {{ currentQuestionIndex + 1 }} of
        {{ quizData.questions.length }}
      </h2>
      <p class="question">{{ currentQuestion.question }}</p>
      <ul class="options__list">
        <li v-for="(option, index) in currentQuestion.options" :key="index">
          <label class="option__label">
            <input
              type="radio"
              :value="index"
              v-model="selectedOptionIndex"
              class="option__input"
            />
            <span class="option__text">{{ option }}</span>
          </label>
        </li>
      </ul>
      <button @click="checkAnswer" class="next__button">Next</button>
    </div>

    <div v-else class="quiz__completed">
      <h2 class="quiz__completed__title">Quiz Completed!</h2>
      <p class="quiz__score">
        You scored {{ score }} out of {{ quizData.questions.length }}
      </p>
      <button @click="resetQuiz" class="reset__button">Start Over</button>
    </div>
  </div>
  
</template>



<script>
  
  export default {
    
    data() {
      return {
        // Define the quiz data
        quizData: {
          title: "My Quiz",
          questions: [
            // Define the first question
            {
              question: "What is the capital of France?",
              options: ["London", "Paris", "Berlin", "Madrid"],
              answerIndex: 1,
            },
            // Define the second question
            {
              question: "What is the highest mountain in the world?",
              options: [
                "Mount Kilimanjaro",
                "Mount Everest",
                "Mount Fuji",
                "Mount McKinley",
              ],
              answerIndex: 1,
            },
            // Define the third question
            {
              question: "Who is the author of 'To Kill a Mockingbird'?",
              options: [
                "J.D. Salinger",
                "F. Scott Fitzgerald",
                "Harper Lee",
                "Ernest Hemingway",
              ],
              answerIndex: 2,
            },
          ],
        },
        // Define the current question index
        currentQuestionIndex: 0,
        // Define the selected option index
        selectedOptionIndex: null,
        // Define the quiz score
        score: 0,
        // Define whether the quiz is completed or not
        quizCompleted: false,
      };
    },
    // Define the computed property to get the current question
    computed: {
      currentQuestion() {
        return this.quizData.questions[this.currentQuestionIndex];
      },
    },
    
    methods: {
      // Define the method to check the answer
      checkAnswer() {
        // Check if an option is selected
        if (this.selectedOptionIndex === null) {
          alert("Please select an option");
          return;
        }
        // Check if the selected option is correct
        if (this.selectedOptionIndex === this.currentQuestion.answerIndex) {
          this.score++;
        }
        // Reset the selected option index
        this.selectedOptionIndex = null;
        // Check if the quiz is completed
        if (this.currentQuestionIndex === this.quizData.questions.length - 1) {
          this.quizCompleted = true;
        } else {
          this.currentQuestionIndex++;
        }
      },
      // Define the method to reset the quiz
      resetQuiz() {
        this.currentQuestionIndex = 0;
        this.selectedOptionIndex = null;
        this.score = 0;
        this.quizCompleted = false;
      },
    },
  };
</script>

<style scoped>
  .quiz {
    display: flex;
  flex-direction: column;
  align-items: flex-start;
  
   
}


  .quiz__title {
    font-size: 2rem;
    margin-bottom: 2rem;
  }

  .quiz__question {
    margin-bottom: 2rem;
  }

  .question__number {
    font-size: 1.5rem;
    font-weight: bold;
    margin-bottom: 1rem;
  }

  .question {
    font-size: 1.2rem;
    margin-bottom: 1rem;
  }

  .options__list {
    list-style: none;
    padding: 0;
    margin: 0 auto;
    max-width: 400px;
  }

  .option__label {
    display: block;
    margin-bottom: 1rem;
    cursor: pointer;
  }

  .option__input {
    display: inline-block;
    margin-right: 0.5rem;
    cursor: pointer;
  }

  .option__text {
    display: inline-block;
    cursor: pointer;
  }

  .next__button {
    font-size: 1rem;
    padding: 0.5rem 1rem;
    margin-top: 1rem;
    background-color: #2196f3;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  .quiz__completed {
    margin-top: 2rem;
  }

  .quiz__completed__title {
    font-size: 1.5rem;
    margin-bottom: 1rem;
  }

  .quiz__score {
    font-size: 1.2rem;
    margin-bottom: 1rem;
  }

  .reset__button {
    font-size: 1rem;
    padding: 0.5rem 1rem;
    background-color: #2196f3;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  @media only screen and (max-width: 600px) {
  .quiz {
    flex-direction: column;
  }
  
  .quiz__question {
    font-size: 1.2rem;
    margin-bottom: 1rem;
  }
  
  .options__list {
    font-size: 1.1rem;
    margin-top: 0.5rem;
  }
  
  .next__button {
    margin-top: 1rem;
  }
  
  .quiz__completed__title {
    font-size: 1.5rem;
    margin-bottom: 1rem;
  }
  
  .quiz__score {
    font-size: 1.2rem;
    margin-bottom: 1rem;
  }
  
  .reset__button {
    margin-top: 1rem;
  }
}

</style>