[View my solution on LeetCode](https://leetcode.com/problems/two-sum/solutions/8284013/a-simple-solution-by-joshuanhmia-mt0p/)

# Intuition

Instead of checking every possible pair of numbers (which would take $O(n^2)$ time), we can look for the "complement" of each number as we iterate through the array. If the `target - current_value` has already been seen, we've found our pair. A hash map allows us to store numbers we've seen (or the complements we need) and look them up almost instantly.

# Approach

1. Initialize an empty hash map (`unordered_map`) called `um`.
2. Iterate through the array `nums` using a loop variable `i`.
3. For each element `nums[i]`, check if it already exists in our map.
* **If it exists:** It means we previously encountered a number that needed *this* current number to reach the target. We return the index stored in the map along with the current index `i`.
* **If it doesn't exist:** We calculate its complement (`target - nums[i]`) and store it in the map as the key, with the current index `i` as the value. This acts as a "looking for" placeholder for future numbers.


4. If no pair is found, return an empty vector `{}` (though the problem guarantees exactly one solution).

# Complexity

* **Time complexity:** $O(n)$
We only traverse the list containing $n$ elements exactly once. Each lookup and insertion in the `unordered_map` takes $O(1)$ time on average.
* **Space complexity:** $O(n)$
In the worst-case scenario, we might store up to $n$ elements in the hash map before finding a match.

# Code

```cpp []
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> um;
        for (int i = 0; i < nums.size(); i++) {
            // If the current number is a needed complement we stored earlier
            if (um.find(nums[i]) != um.end()) {
                return {um[nums[i]], i};
            } else {
                // Store the complement we need, mapping it to the current index
                um[target - nums[i]] = i;
            }
        }
        return {};
    }
};

```
