# Code1
#include <iostream>
#include <vector>
using namespace std;

bool isSafe(vector<string>& mat, int row, int col, int n) {
    for (int j = 0; j < n; j++)
        if (mat[row][j] == 'Q') return false;

    for (int i = 0; i < n; i++)
        if (mat[i][col] == 'Q') return false;

    for (int i = row, j = col; i >= 0 && j >= 0; i--, j--)
        if (mat[i][j] == 'Q') return false;

    for (int i = row, j = col; i >= 0 && j < n; i--, j++)
        if (mat[i][j] == 'Q') return false;

    return true;
}

void nQueens(vector<string>& mat, int row, int n, vector<vector<string>>& ans) {
    if (row == n) {
        ans.push_back(mat);
        return;
    }

    for (int j = 0; j < n; j++) {
        if (isSafe(mat, row, j, n)) {
            mat[row][j] = 'Q';
            nQueens(mat, row + 1, n, ans);
            mat[row][j] = '.'; // Backtracking step
        }
    }
}

vector<vector<string>> SolveNQueens(int n) {
    vector<string> mat(n, string(n, '.'));
    vector<vector<string>> ans;
    nQueens(mat, 0, n, ans);
    return ans;
}

int main() {
    int n = 4;
    vector<vector<string>> solutions = SolveNQueens(n);
    for (const auto& result : solutions) {
        for (const auto& row : result) {
            cout << row << endl;
        }
        cout << endl;
    }
    return 0;
}
