# online-quiz-application
The Online Quiz Application is a console-based quiz system. 
Here's a basic implementation of an online quiz using Java:
Here's a simple online quiz code in Java using GUI (Graphical User Interface) with Swing library:


import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.ArrayList;

public class OnlineQuiz {
    JFrame frame;
    JLabel questionLabel;
    JRadioButton option1, option2, option3, option4;
    JButton submitButton, nextButton;
    ButtonGroup group;
    int score, currentQuestion;
    ArrayList<Question> questions;

    public OnlineQuiz() {
        createGUI();
        loadQuestions();
        displayQuestion();
    }

    void createGUI() {
        frame = new JFrame("Online Quiz");
        frame.setSize(400, 300);
        frame.setLayout(new BorderLayout());
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        questionLabel = new JLabel();
        questionLabel.setFont(new Font("Arial", Font.BOLD, 16));
        frame.add(questionLabel, BorderLayout.NORTH);

        JPanel optionsPanel = new JPanel();
        optionsPanel.setLayout(new GridLayout(4, 1));
        frame.add(optionsPanel, BorderLayout.CENTER);

        option1 = new JRadioButton();
        option1.setFont(new Font("Arial", Font.PLAIN, 14));
        optionsPanel.add(option1);

        option2 = new JRadioButton();
        option2.setFont(new Font("Arial", Font.PLAIN, 14));
        optionsPanel.add(option2);

        option3 = new JRadioButton();
        option3.setFont(new Font("Arial", Font.PLAIN, 14));
        optionsPanel.add(option3);

        option4 = new JRadioButton();
        option4.setFont(new Font("Arial", Font.PLAIN, 14));
        optionsPanel.add(option4);

        group = new ButtonGroup();
        group.add(option1);
        group.add(option2);
        group.add(option3);
        group.add(option4);

        JPanel buttonPanel = new JPanel();
        frame.add(buttonPanel, BorderLayout.SOUTH);

        submitButton = new JButton("Submit");
        submitButton.addActionListener(this::checkAnswer);
        buttonPanel.add(submitButton);

        nextButton = new JButton("Next");
        nextButton.addActionListener(this::displayNextQuestion);
        nextButton.setEnabled(false);
        buttonPanel.add(nextButton);

        frame.setVisible(true);
    }

    void loadQuestions() {
        questions = new ArrayList<>();
        questions.add(new Question("What is the capital of France?", "Paris", "London", "Berlin", "Rome"));
        questions.add(new Question("Who is the founder of Microsoft?", "Bill Gates", "Steve Jobs", "Mark Zuckerberg", "Jeff Bezos"));
        questions.add(new Question("What is the largest planet in our solar system?", "Jupiter", "Earth", "Saturn", "Uranus"));
    }

    void displayQuestion() {
        if (currentQuestion < questions.size()) {
            Question question = questions.get(currentQuestion);
            questionLabel.setText(question.getQuestion());
            option1.setText(question.getOption1());
            option2.setText(question.getOption2());
            option3.setText(question.getOption3());
            option4.setText(question.getOption4());
            group.clearSelection();
            submitButton.setEnabled(true);
            nextButton.setEnabled(false);
        } else {
            displayResult();
        }
    }

    void checkAnswer(ActionEvent e) {
        JRadioButton selected = group.getSelected();
        if (selected != null) {
            Question question = questions.get(currentQuestion);
            if (selected.getText().equals(question.getAnswer())) {
                score++;
            }
            submitButton.setEnabled(false);
            nextButton.setEnabled(true);
        }
    }

    void displayNextQuestion(ActionEvent e) {
        currentQuestion++;
        displayQuestion();
    }

    void displayResult() {
        questionLabel.setText("Quiz Finished!");
        option1.setVisible(false);
        option2.setVisible(false);
        option3.setVisible(false);
        option4.setVisible(false);
        submitButton.setVisible(false);
        nextButton.setVisible(false);
        JOptionPane.showMessageDialog(frame, "Your score is " + score + "/" + questions.size());
        System.exit(0);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(OnlineQuiz::new);
    }
}

class Question {
    private String question;
    private String answer;
    private String option1;
    private String option2;
    private String option3;

    public Question(String question, String answer, String option2, String option3, String option4) {
        this.question = question;
        this.answer = answer;
        this.option1 = answer;
        this.option2 = option2;
        this.option3 = option3;
        // Randomly shuffle options
        String[] options = {option1, option2, option3, option4};
        // Implement shuffle logic
    }

    public String getQuestion() {
        return question;
    }

    public String getAnswer() {
        return answer;
    }

    public String getOption1() {
        return option1;
    }

    public String getOption2() {
        return option2;
    }

    public String getOption3() {
        return option3


