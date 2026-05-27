
Leetcode: 3121. Count the Number of Special Characters II

Problem:
A letter c is called special if:
1. It appears in both lowercase and uppercase.
2. Every lowercase occurrence appears before the first uppercase occurrence.

Return the number of special letters.

Approach:
- Store the last occurrence index of every lowercase character.
- Store the first/last occurrence of uppercase characters.
- For every lowercase character:
    If its uppercase version exists
    and last lowercase index < first uppercase index,
    then it is a special character.

Time Complexity: O(N)
Space Complexity: O(1)


class Solution {
public:
    int numberOfSpecialChars(string word) {

        unordered_map<char, int> lower;
        unordered_map<char, int> upper;

        int n = word.size();

        for (int i = 0; i < n; i++) {

            char ch = word[i];

            if (ch >= 'a' && ch <= 'z') {
                lower[ch] = i;   
            }
            else {

                // store first uppercase occurrence
                if (!upper.count(ch)) {
                    upper[ch] = i;
                }
            }
        }

        int cnt = 0;

        for (auto &it : lower) {

            char lowerChar = it.first;
            int lowerIndex = it.second;

            char upperChar = lowerChar - 'a' + 'A';

            if (upper.count(upperChar) &&
                lowerIndex < upper[upperChar]) {

                cnt++;
            }
        }

        return cnt;
    }
};