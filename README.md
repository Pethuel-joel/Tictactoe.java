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
