import java.util.Scanner;
public class TicTacToe {
    private static char[][] board;
    private static final int SIZE = 3;
    private static char currentPlayer;
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean playAgain = true;
        while (playAgain) {
            initializeBoard();
            currentPlayer = 'X';
            boolean gameWon = false;
            int movesCount = 0;
            while (!gameWon && movesCount < SIZE * SIZE) {
                printBoard();
                System.out.println("Player " + currentPlayer + ", enter your move (row and column): ");
                int row = scanner.nextInt() - 1;
                int col = scanner.nextInt() - 1;
                if (isValidMove(row, col)) {
                    board[row][col] = currentPlayer;
                    movesCount++;
                    if (checkWin(row, col)) {
                        gameWon = true;
                        printBoard();
                        System.out.println("Player " + currentPlayer + " wins!");
                    } else if (movesCount == SIZE * SIZE) {
                        printBoard();
                        System.out.println("It's a draw!");
                    } else {
                        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
                    }
                } else {
                    System.out.println("This move is not valid. Try again.");
                }
            }
            System.out.println("Do you want to play again? (yes/no)");
            playAgain = scanner.next().equalsIgnoreCase("yes");
        }
    }
    private static void initializeBoard() {
        board = new char[SIZE][SIZE];
        for (int i = 0; i < SIZE; i++) {
            for (int j = 0; j < SIZE; j++) {
                board[i][j] = '-';
            }
        }
    }
    private static void printBoard() {
        for (int i = 0; i < SIZE; i++) {
            for (int j = 0; j < SIZE; j++) {
                System.out.print(board[i][j] + " ");
            }
            System.out.println();
        }
    }
    private static boolean isValidMove(int row, int col) {
        return row >= 0 && row < SIZE && col >= 0 && col < SIZE && board[row][col] == '-';
    }
    private static boolean checkWin(int row, int col) {
        if (board[row][0] == currentPlayer && board[row][1] == currentPlayer && board[row][2] == currentPlayer) {
            return true;
        }
        if (board[0][col] == currentPlayer && board[1][col] == currentPlayer && board[2][col] == currentPlayer) {
            return true;
        }
        if (row == col && board[0][0] == currentPlayer && board[1][1] == currentPlayer && board[2][2] == currentPlayer) {
            return true;
        }
        if (row + col == SIZE - 1 && board[0][2] == currentPlayer && board[1][1] == currentPlayer && board[2][0] == currentPlayer) {
            return true;
        }
        return false;
    }
}
