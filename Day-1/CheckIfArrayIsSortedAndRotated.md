# 🔄 Check if Array Is Sorted and Rotated

## 📝 Problem Statement
Given an array `nums`, return `true` if the array was originally sorted in non-decreasing order and then rotated some number of positions. Otherwise, return `false`.

---

# 🧠 Brute Force Approach

## 💡 Idea
- Create a sorted copy of the array.
- Find the breaking point where:
```cpp
nums[i] > nums[i+1]

Rotate the array back using reversal algorithm.
Compare the final array with the sorted copy.

Brute force code

class Solution {
public:
    bool check(vector<int>& nums) {
        int n = nums.size();

        vector<int> copy(nums.begin(), nums.end());
        sort(copy.begin(), copy.end());

        int pivot = -1;

        for(int i = 0; i < n - 1; i++) {
            if(nums[i] > nums[i + 1]) {
                pivot = i;
                break;
            }
        }

        if(pivot == -1) return true;

        reverse(nums.begin(), nums.begin() + pivot + 1);
        reverse(nums.begin() + pivot + 1, nums.end());
        reverse(nums.begin(), nums.end());

        return nums == copy;
    }
};

⏱️ Time Complexity
Sorting - O(n log n)
Reversals + Comparison - O(n)
Overall- O(n log n)

📦 Space Complexity- O(n)  (Extra array is used for storing the sorted copy.)

⚡ Optimal Approach
💡 Observation

In a sorted and rotated array, the order can break at most once.

We count how many times: nums[i] > nums[(i+1)%n]
If the count becomes greater than 1, the array is not sorted and rotated.

CODE

class Solution {
public:
    bool check(vector<int>& nums) {
        int n = nums.size();
        int cnt = 0;

        for(int i = 0; i < n; i++) {
            if(nums[i] > nums[(i + 1) % n]) {
                cnt++;
            }
        }

        return cnt <= 1;
    }
};

⏱️ Time Complexity - O(n)
📦 Space Complexity - O(1)