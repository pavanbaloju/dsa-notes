### Problem Statement

Link: https://leetcode.com/problems/valid-sudoku/description/

### Brute Force Approach


### Solution
```java
public class ValidSudokuBruteForce {
    public boolean isValidSudoku(char[][] board) {
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] != '.' && !isValid(board, i, j)) {
                    return false;
                }
            }
        }
        return true;
    }

    private boolean isValid(char[][] board, int row, int col) {
        char num = board[row][col];

        // Check row
        for (int j = 0; j < 9; j++) {
            if (j != col && board[row][j] == num) {
                return false;
            }
        }

        // Check column
        for (int i = 0; i < 9; i++) {
            if (i != row && board[i][col] == num) {
                return false;
            }
        }

        // Check sub-grid
        int startRow = (row / 3) * 3;
        int startCol = (col / 3) * 3;
        for (int i = startRow; i < startRow + 3; i++) {
            for (int j = startCol; j < startCol + 3; j++) {
                if ((i != row || j != col) && board[i][j] == num) {
                    return false;
                }
            }
        }

        return true;
    }
}

```

### Complexity analysis


### Better Approach


### Solution
```java
import java.util.HashSet;

public class ValidSudoku {

    public boolean isValidSudoku(char[][] board) {
        HashSet<String> visited = new HashSet<>(); // Hash set to track visited elements

        for (int i = 0; i < 9; i++) { // Iterate through each row
            for (int j = 0; j < 9; j++) { // Iterate through each column
                // Skip empty cells
                if (board[i][j] == '.') continue;

                // Generate unique identifiers for rows, columns, and sub-boxes
                String num = String.valueOf(board[i][j]); // Convert char to string
                if (!visited.add(num + "@row" + i) ||                 // Check row
                    !visited.add(num + "@col" + j) ||                 // Check column
                    !visited.add(num + "@box" + (i / 3) + (j / 3))) { // Check sub-box
                    return false; // Duplicate found
                }
            }
        }
        return true; // No duplicates found
    }

    public static void main(String[] args) {
        char[][] board = {
            {'5', '3', '.', '.', '7', '.', '.', '.', '.'},
            {'6', '.', '.', '1', '9', '5', '.', '.', '.'},
            {'.', '9', '8', '.', '.', '.', '.', '6', '.'},
            {'8', '.', '.', '.', '6', '.', '.', '.', '3'},
            {'4', '.', '.', '8', '.', '3', '.', '.', '1'},
            {'7', '.', '.', '.', '2', '.', '.', '.', '6'},
            {'.', '6', '.', '.', '.', '.', '2', '8', '.'},
            {'.', '.', '.', '4', '1', '9', '.', '.', '5'},
            {'.', '.', '.', '.', '8', '.', '.', '7', '9'}
        };

        ValidSudoku validator = new ValidSudoku();
        System.out.println("Is the Sudoku board valid? " + validator.isValidSudoku(board));
    }
}

```

### Complexity analysis


### Optimal Approach


### Solution
```java
public class ValidSudoku {

    public boolean isValidSudoku(char[][] board) {
        boolean[][] rowDigit = new boolean[9][9]; // Boolean array for rows
        boolean[][] colDigit = new boolean[9][9]; // Boolean array for columns
        boolean[][][] boxDigit = new boolean[3][3][9]; // Boolean array for sub-boxes

        for (int i = 0; i < 9; i++) { // Iterate through each row
            for (int j = 0; j < 9; j++) { // Iterate through each column
                if (board[i][j] != '.') { // Skip empty cells
                    int digit = board[i][j] - '1'; // Convert char to int index (0 to 8)

                    // Check if the digit already exists in the current row
                    if (rowDigit[i][digit]) {
                        return false; // Digit already exists in the row
                    }
                    rowDigit[i][digit] = true; // Mark the digit as seen in the row

                    // Check if the digit already exists in the current column
                    if (colDigit[j][digit]) {
                        return false; // Digit already exists in the column
                    }
                    colDigit[j][digit] = true; // Mark the digit as seen in the column

                    // Check if the digit already exists in the current 3x3 sub-box
                    if (boxDigit[i / 3][j / 3][digit]) {
                        return false; // Digit already exists in the sub-box
                    }
                    boxDigit[i / 3][j / 3][digit] = true; // Mark the digit as seen in the sub-box
                }
            }
        }

        return true; // No duplicates found
    }

    public static void main(String[] args) {
        char[][] board = {
            {'5', '3', '.', '.', '7', '.', '.', '.', '.'},
            {'6', '.', '.', '1', '9', '5', '.', '.', '.'},
            {'.', '9', '8', '.', '.', '.', '.', '6', '.'},
            {'8', '.', '.', '.', '6', '.', '.', '.', '3'},
            {'4', '.', '.', '8', '.', '3', '.', '.', '1'},
            {'7', '.', '.', '.', '2', '.', '.', '.', '6'},
            {'.', '6', '.', '.', '.', '.', '2', '8', '.'},
            {'.', '.', '.', '4', '1', '9', '.', '.', '5'},
            {'.', '.', '.', '.', '8', '.', '.', '7', '9'}
        };

        ValidSudoku validator = new ValidSudoku();
        System.out.println("Is the Sudoku board valid? " + validator.isValidSudoku(board));
    }
}

```

### Complexity analysis


### Attachments
![[Pasted image 20250113122109.png]]
![[Pasted image 20250113122117.png]]
![[Pasted image 20250113122126.png]]

### Tags
[[Matrix]] [[Hashing]]

### References
[[Matrix Traversal Formulae]]