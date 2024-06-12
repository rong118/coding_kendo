# Backtracking

Backtracking is a general algorithmic technique used in computer science for solving problems incrementally, one piece at a time, and removing solutions that fail to satisfy the constraints of the problem at any point of time (i.e., constraints that are violated).

It is often employed in scenarios where there are multiple potential solutions, and the goal is to find one or all solutions that satisfy the given conditions.

## Key Characterist
- **Incremental Construction:** Build the solution step by step.
- **Constraints Checking**: At each step, check if the current partial solution is valid under the problem's constraints.
- **Backtrack**: If the current partial solution violates constraints or doesn't lead to a solution, discard it (backtrack) and try another path.

## Example: N-Queens Problem

The N-Queens problem involves placing N queens on an N×N chessboard such that no two queens threaten each other. 

Here's a high-level approach to solving it using backtracking:
- Place a queen in the first column of the first row.
- Move to the next row and place a queen in a column where it is not threatened by the previous queens.
- Continue this process row by row.
- If placing a queen in any column of a row is not possible (because it would be threatened), backtrack to the previous row and move the queen to the next possible column.
- Repeat until all queens are placed or all configurations have been tried.

### C++ Implementation
```c++
#include <iostream>
#include <vector>

using namespace std;

class NQueens {
public:
    NQueens(int n) : size(n), board(n, vector<int>(n, 0)) {}

    void solve() {
        placeQueen(0);
    }

private:
    int size;
    vector<vector<int>> board;

    void printSolution() {
        for (const auto& row : board) {
            for (int cell : row) {
                cout << (cell ? "Q" : ".") << " ";
            }
            cout << endl;
        }
        cout << endl;
    }

    bool isSafe(int row, int col) {
        // Check the column
        for (int i = 0; i < row; ++i) {
            if (board[i][col]) {
                return false;
            }
        }

        // Check the upper left diagonal
        for (int i = row, j = col; i >= 0 && j >= 0; --i, --j) {
            if (board[i][j]) {
                return false;
            }
        }

        // Check the upper right diagonal
        for (int i = row, j = col; i >= 0 && j < size; --i, ++j) {
            if (board[i][j]) {
                return false;
            }
        }

        return true;
    }

    bool placeQueen(int row) {
        if (row == size) {
            printSolution();
            return true;
        }

        bool foundSolution = false;

        for (int col = 0; col < size; ++col) {
            if (isSafe(row, col)) {
                board[row][col] = 1; // Place the queen

                // Recursively place queens in the next row
                foundSolution = placeQueen(row + 1) || foundSolution;

                board[row][col] = 0; // Backtrack and remove the queen
            }
        }

        return foundSolution;
    }
};

int main() {
    int n;
    cout << "Enter the value of N for the N-Queens problem: ";
    cin >> n;

    NQueens nQueens(n);
    nQueens.solve();

    return 0;
}
```

### Runtime Complexity
The worst-case time complexity of the N-Queens problem using backtracking is O(N^N).
