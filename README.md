# BackTracking
#include<iostream>
using namespace std;
bool isSafe(int row ,int col ,vector<vector<int>> &board ,int n){
    int x = row;
    int y = col;
    while(y>=0){
        if(board[x][y]==1)
            return false;
        y--;
    }
    x = row ;
    y = col;
    while( x >= 0 && y>=0){
        if(board[x][y]==1)
            return false;
        x--;
        y--;
    }
    x = row;
    y = col;
    while(x<n && y>=0){
        if(board[x][y]==1)
            return false;
        x++;
        y--;
    }
}
void addSolution(vector<vector<int>> &ans ,vector<vector<int>> &board ,int n){
    vector<int>temp;
    for(int i = 0 ; i<n ; i++){
     for(int j= 0 ; j<n ;j++){
         temp.push_back(board[i][j]);
     }
    }
    ans.push_back(temp);
}

void solve(int col , vector<vector<int>>&board ,vector<vector<int>>&ans ,int n){
    if(col == n){
        addSolution(ans,board,n);
        return;
    }
    for(int row = 0 ; row <n ; row++){
        if(isSafe(row,col,board,n)){
            board[row][col] = 1;
            solve(col+1,board,ans,n);
            board[row][col] = 0;
        }
    }
    
}
int main(){
    int n = 4;
    vector<vector<int>> ans = solveNQueens(n);
    return 0;
}

vector<vector<int>> solveNQueens(int n) {
    // Write your code here.
    vector<vector<int>> ans;
    vector<vector<int>>board(n,vector<int>(n,0));
    solve(0,board,ans,n);
    return ans;
}
