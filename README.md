# LeetCode-1079

# C++

class Solution {
public:
    void func(string tiles,string a,map<string,int>&mp,vector<int>used)
    {
        if(a.length())
        mp[a]=1;
        for(int i=0;i<tiles.length();i++)
        {
            if(used[i]==0)
            {
                used[i]=1;
                a+=tiles[i];
                func(tiles,a,mp,used);
                used[i]=0;
                a.pop_back();
            }
        }
        return;
    }
    int numTilePossibilities(string tiles) {
        map<string,int>mp;
        string a="";
        vector<int>used(tiles.size(),0);
        func(tiles,a,mp,used);
        return mp.size();
    }
};

# Java

import java.util.HashSet;

class Solution {
    private HashSet<String> uniqueCombinations = new HashSet<>();

    private void func(String tiles, String current, boolean[] used) {
        if (!current.isEmpty()) {
            uniqueCombinations.add(current);
        }
        
        for (int i = 0; i < tiles.length(); i++) {
            if (!used[i]) {
                used[i] = true;
                func(tiles, current + tiles.charAt(i), used);
                used[i] = false;  // Backtracking
            }
        }
    }

    public int numTilePossibilities(String tiles) {
        boolean[] used = new boolean[tiles.length()];
        func(tiles, "", used);
        return uniqueCombinations.size();
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.numTilePossibilities("AAB")); // Output: Number of unique sequences
    }
}

# Python

class Solution:
    def __init__(self):
        self.unique_combinations = set()
    
    def func(self, tiles, current, used):
        if current:
            self.unique_combinations.add(current)
        
        for i in range(len(tiles)):
            if not used[i]:
                used[i] = 1
                self.func(tiles, current + tiles[i], used)
                used[i] = 0  # Backtracking
    
    def numTilePossibilities(self, tiles: str) -> int:
        used = [0] * len(tiles)
        self.func(tiles, "", used)
        return len(self.unique_combinations)

# Example Usage:
solution = Solution()
print(solution.numTilePossibilities("AAB"))  # Output: Number of unique sequences
