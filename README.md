# Quiz App

This project is a simple quiz application that allows users to answer multiple-choice questions and receive feedback on their performance. The app is built using HTML, CSS, and JavaScript.

## Features

- Multiple-choice questions
- Real-time feedback on answers
- Score tracking
- Responsive design

## How It Works

The app displays a series of questions one at a time. Users select an answer for each question and receive immediate feedback on whether their answer is correct or incorrect. The app keeps track of the user's score and displays it at the end of the quiz.

## Code Explanation

### HTML

The HTML structure includes containers for the quiz question, answer choices, and feedback. Here's a basic example:

```html
<div id="quiz-container">
    <div id="question"></div>
    <div id="answer-buttons" class="btn-container"></div>
    <button id="next-btn" class="next-btn btn">Next</button>
</div>
```
### JavaScript
The JavaScript code handles the logic for displaying questions, checking answers, updating the score, and managing the next steps. Here's the full code:

```javascript
const questions = [
    {
        question: "Which is the largest animal in the world?",
        answers: [
            { text: "Shark", correct: false },
            { text: "Blue Whale", correct: true },
            { text: "Elephant", correct: false },
            { text: "Giraffe", correct: false },
        ]
    },
    {
        question: "Which is the smallest country in the world?",
        answers: [
            { text: "Vatican City", correct: true },
            { text: "Bhutan", correct: false },
            { text: "Nepal", correct: false },
            { text: "Sri Lanka", correct: false },
        ]
    },
    {
        question: "Which is the largest desert in the world?",
        answers: [
            { text: "Kalahari", correct: false },
            { text: "Gobi", correct: false },
            { text: "Sahara", correct: true },
            { text: "Thar", correct: false },
        ]
    },
    {
        question: "Which is the smallest continent in the world?",
        answers: [
            { text: "Asia", correct: false },
            { text: "Arctic", correct: false },
            { text: "Africa", correct: false },
            { text: "Australia", correct: true },
        ]
    }
];

const questionElement = document.getElementById("question");
const answerButtons = document.getElementById("answer-buttons");
const nextButton = document.getElementById("next-btn");

let currentQuestionIndex = 0;
let score = 0;

function startQuiz() {
    currentQuestionIndex = 0;
    score = 0;
    nextButton.innerHTML = "Next";
    showQuestion();
}

function showQuestion() {
    resetState();
    let currentQuestion = questions[currentQuestionIndex];
    let questionNo = currentQuestionIndex + 1;
    questionElement.innerHTML = questionNo + ". " + currentQuestion.question;

    currentQuestion.answers.forEach(answer => {
        const button = document.createElement("button");
        button.innerHTML = answer.text;
        button.classList.add("btn");
        answerButtons.appendChild(button);
        if (answer.correct) {
            button.dataset.correct = answer.correct;
        }
        button.addEventListener("click", selectAnswer);
    });
}

function resetState() {
    nextButton.style.display = "none";
    while (answerButtons.firstChild) {
        answerButtons.removeChild(answerButtons.firstChild);
    }
}

function selectAnswer(e) {
    const selectBtn = e.target;
    const isCorrect = selectBtn.dataset.correct === "true";
    if (isCorrect) {
        selectBtn.classList.add("correct");
        score++;
    } else {
        selectBtn.classList.add("incorrect");
    }
    Array.from(answerButtons.children).forEach(button => {
        if (button.dataset.correct === "true") {
            button.classList.add("correct");
        }
        button.disabled = true;
    });
    nextButton.style.display = "block";
}

function showScore() {
    resetState();
    questionElement.innerHTML = `You scored ${score} out of ${questions.length}!`;
    nextButton.innerHTML = "Play Again";
    nextButton.style.display = "block";
}

function handleNextButton() {
    currentQuestionIndex++;
    if (currentQuestionIndex < questions.length) {
        showQuestion();
    } else {
        showScore();
    }
}

nextButton.addEventListener("click", () => {
    if (currentQuestionIndex < questions.length) {
        handleNextButton();
    } else {
        startQuiz();
    }
});

startQuiz();
```

## Explanation
This section provides a detailed explanation of how the code works:

1. HTML Structure: Contains the elements for displaying questions, answer buttons, and the next button.
2. JavaScript Logic: Handles displaying questions, checking answers, updating the score, and managing the next steps.

- **startQuiz()**: Initializes the quiz.
- **showQuestion()**: Displays the current question and answer choices.
- **resetState()**: Resets the state for the next question.
- **selectAnswer(e)**: Checks if the selected answer is correct and updates the feedback.
- **showScore()**: Displays the user's score at the end of the quiz.
- **handleNextButton()**: Moves to the next question or shows the score if the quiz is complete.

## Contributing
If you'd like to contribute to this project, please fork the repository and submit a pull request.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
