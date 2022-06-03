# GFG-DAY-01
Rat Maze With Multiple Jumps
Rat Maze With Multiple Jumps 
Medium Accuracy: 58.4% Submissions: 6116 Points: 4
A Maze is given as n*n matrix of blocks where source block is the upper left most block i.e., matrix[0][0] and destination block is lower rightmost block i.e., matrix[n-1][n-1]. A rat starts from source and has to reach the destination. The rat can move in only two directions: first forward if possible or down. If multiple solutions exist, the shortest earliest hop will be accepted. For the same hop distance at any point, forward will be preferred over downward. In the maze matrix, 0 means the block is the dead end and non-zero number means the block can be used in the path from source to destination. The non-zero value of mat[i][j] indicates number of maximum jumps rat can make from cell mat[i][j]. In this variation, Rat is allowed to jump multiple steps at a time instead of 1. Find a matrix which describes the position the rat to reach at the destination.
 

Example:

Input: {{2,1,0,0},{3,0,0,1},{0,1,0,1},
{0,0,0,1}}
Output: {{1,0,0,0},{1,0,0,1},{0,0,0,1},
{0,0,0,1}}
Explanation: Rat started with matrix[0][0] and 
can jump up to 2 steps right/down. First check 
matrix[0][1] as it is 1, next check 
matrix[0][2] ,this won't lead to the solution. 
Then check matrix[1][0], as this is 3(non-zero)
,so we can make 3 jumps to reach matrix[1][3]. 
From matrix[1][3] we can move downwards taking 
1 jump each time to reach destination at 
matrix[3][3].
Example 2:

Input: {{2,1,0,0},{2,0,0,1},{0,1,0,1},
{0,0,0,1}}
Output: {{-1}}
Explanation: As no path exists so, -1.
 

Your Task:
You don't need to read or print anyhting, Your task is to complete the function ShortestDistance() which takes the matrix as input parameter and returns a matrix of size n if path exists otherwise returns a matrix of 1x1 which contains -1. In output matrix, 1 at (i, j) represents the cell is taken into the path otherwise 0 if any path exists.
 

Expected Time Complexity: O(n*n*k) where k is max(matrix[i][j])
Expected Space Complexity: O(1)
 

Constraints:
1 <= n <= 50
1 <= matrix[i][j] <= 20

View Bookmarked Problems
Topic Tags

________________________________________________________________________________________________________________________________________________________
// { Driver Code Starts
#include<bits/stdc++.h>
using namespace std;

 // } Driver Code Ends
class Solution {
public:
bool calc(vector<vector<int>>&matrix,vector<vector<int>>&ans,int i,int j){
    int n =matrix.size();
    if(i>=n||j>=n)return false;
    ans[i][j]=1;
    if(i==n-1 && j==n-1)return true;
    int jumps =matrix[i][j];
    for(int k =1;k<=jumps;k++){
        if(calc(matrix,ans,i,j+k))return true;
        if(calc(matrix,ans,i+k,j))return true;
    }
    ans[i][j]=0;
    return false;
}
	vector<vector<int>> ShortestDistance(vector<vector<int>>&matrix){
	 int n=matrix.size();
	 vector<vector<int>>ans(n,vector<int>(n,0));
	 if (calc(matrix,ans,0,0))
        return ans;
	 
	else 
	    return {{-1}};
	
	
	}
/*{2,1,0,0}
{3,0,0,1}
{0,1,0,1}
{0,0,0,1}*/
/*1 0 0 0
  1 0 0 1
  0 0 0 1
  0 0 0 1
*/
};

// { Driver Code Starts.
int main(){
	int tc;
	cin >> tc;
	while(tc--){
		int n;
		cin >> n;
		vector<vector<int>>matrix(n, vector<int>(n,0));
		for(int i = 0; i < n; i++){
			for(int j = 0; j < n; j++){
				cin >> matrix[i][j];
			}
		}
		Solution obj;
		vector<vector<int>> ans = obj.ShortestDistance(matrix);
		for(auto i: ans){
			for(auto j: i){
				cout << j << " ";
			}
			cout << "\n";
		}
	}
	return 0;
}  // } Driver Code Ends







