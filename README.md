# online-quiz-application
The Online Quiz Application is a console-based quiz system. 
Here's a basic implementation of an online quiz using Java:


Quiz.java

import java.util.*;

public class Quiz {
    private List<Question> questions;
    private int score;

    public Quiz() {
        questions = new ArrayList<>();
        score = 0;
    }

    public void addQuestion(String question, String[] options, int correctAnswer) {
        questions.add(new Question(question, options, correctAnswer));
    }

    public void startQuiz() {
        Scanner scanner = new Scanner(System.in);

        for (Question question : questions) {
            System.out.println(question.getQuestion());
            for (int i = 0; i < question.getOptions().length; i++) {
                System.out.println((i + 1) + ". " + question.getOptions()[i]);
            }

            System.out.print("Enter your answer (1-" + question.getOptions().length + "): ");
            int answer = scanner.nextInt();

            if (answer == question.getCorrectAnswer()) {
                score++;
                System.out.println("Correct!");
            } else {
                System.out.println("Incorrect. Correct answer: " + question.getOptions()[question.getCorrectAnswer() - 1]);
            }
        }

        System.out.println("Quiz finished. Your score: " + score + "/" + questions.size());
    }

    public static void main(String[] args) {
        Quiz quiz = new Quiz();

        quiz.addQuestion("What is the capital of France?", new String[]{"Paris", "London", "Berlin", "Rome"}, 1);
        quiz.addQuestion("Who is the CEO of Tesla?", new String[]{"Elon Musk", "Jeff Bezos", "Bill Gates", "Mark Zuckerberg"}, 1);
        quiz.addQuestion("What is the largest planet in our solar system?", new String[]{"Jupiter", "Earth", "Saturn", "Uranus"}, 1);

        quiz.startQuiz();
    }
}

class Question {
    private String question;
    private String[] options;
    private int correctAnswer;

    public Question(String question, String[] options, int correctAnswer) {
        this.question = question;
        this.options = options;
        this.correctAnswer = correctAnswer;
    }

    public String getQuestion() {
        return question;
    }

    public String[] getOptions() {
        return options;
    }

    public int getCorrectAnswer() {
        return correctAnswer;
    }
}

