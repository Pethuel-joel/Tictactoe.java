import javax.swing.*;
import java.awt.*;


public class TicTacToe extends JFrame {
    private final CardLayout cardLayout = new CardLayout();
    private final JPanel mainPanel = new JPanel(cardLayout);

    private final JTextField player1Field = new JTextField(10);
    private final JTextField player2Field = new JTextField(10);
    private String player1Name = "Player 1";
    private String player2Name = "Player 2";

    private final JButton[][] buttons = new JButton[3][3];
    private boolean xTurn = true;
    private int moves = 0;

    public TicTacToe() {
        setTitle("Tic Tac Toe Deluxe");
        setSize(400, 500);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        mainPanel.add(createWelcomeScreen(), "Welcome");
        mainPanel.add(createGameScreen(), "Game");

        add(mainPanel);
        cardLayout.show(mainPanel, "Welcome");
    }
private JPanel createWelcomeScreen() {
        JPanel welcome = new JPanel();
        welcome.setLayout(new BoxLayout(welcome, BoxLayout.Y_AXIS));
        welcome.setBackground(Color.WHITE);

        JLabel title = new JLabel("Welcome to Tic Tac Toe Deluxe!");
        title.setFont(new Font("SansSerif", Font.BOLD, 20));
        title.setAlignmentX(Component.CENTER_ALIGNMENT);

        welcome.add(Box.createVerticalStrut(40));
        welcome.add(title);
        welcome.add(Box.createVerticalStrut(30));

        JPanel inputPanel = new JPanel(new GridLayout(2, 2, 10, 10));
        inputPanel.add(new JLabel("Player 1 Name (X):"));
        inputPanel.add(player1Field);
        inputPanel.add(new JLabel("Player 2 Name (O):"));
        inputPanel.add(player2Field);

        welcome.add(inputPanel);

        JButton continueBtn = new JButton("Continue to Game");
        continueBtn.setAlignmentX(Component.CENTER_ALIGNMENT);
        continueBtn.addActionListener(e -> {
            player1Name = player1Field.getText().trim().isEmpty() ? "Player 1" : player1Field.getText().trim();
            player2Name = player2Field.getText().trim().isEmpty() ? "Player 2" : player2Field.getText().trim();
            resetGame();
            cardLayout.show(mainPanel, "Game");
        });
welcome.add(Box.createVerticalStrut(20));

        welcome.add(continueBtn);


        return welcome;

    }



    private JPanel createGameScreen() {

        JPanel gamePanel = new JPanel(new BorderLayout());



        JPanel boardPanel = new JPanel(new GridLayout(3, 3));

        Font btnFont = new Font("Arial", Font.BOLD, 40);



        for (int i = 0; i < 3; i++) {

            for (int j = 0; j < 3; j++) {

                JButton btn = new JButton("");

                btn.setFont(btnFont);

                final int row = i, col = j;

                btn.addActionListener(e -> handleMove(btn, row, col));

                buttons[i][j] = btn;

                boardPanel.add(btn);

            }

        }



        JButton restartBtn = new JButton("Restart");

        restartBtn.addActionListener(e -> {

            resetGame();

        });



        JPanel bottomPanel = new JPanel();

        bottomPanel.add(restartBtn);                                                                                                                                                       
gamePanel.add(boardPanel, BorderLayout.CENTER);
        gamePanel.add(bottomPanel, BorderLayout.SOUTH);

        return gamePanel;
    }

    private void handleMove(JButton btn, int row, int col) {
        if (!btn.getText().isEmpty()) return;

        btn.setText(xTurn ? "X" : "O");
        moves++;

        if (checkWinner()) {
            String winner = xTurn ? player1Name : player2Name;
            JOptionPane.showMessageDialog(this, winner + " wins!");
            resetGame();
        } else if (moves == 9) {
            JOptionPane.showMessageDialog(this, "It's a draw!");
            resetGame();
        } else {
            xTurn = !xTurn;
        }
    }

    private boolean checkWinner() {
        String symbol = xTurn ? "X" : "O";

        // Rows and columns
        for (int i = 0; i < 3; i++) {       
