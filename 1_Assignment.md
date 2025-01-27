OOP Question

Question 1
LEETCODE 705. Design HashSet
Design a HashSet without using any built-in hash table libraries.
Implement MyHashSet class:
void add(key) Inserts the value key into the HashSet.
bool contains(key) Returns whether the value key exists in the HashSet or not.
void remove(key) Removes the value key in the HashSet. If key does not exist in the HashSet, do nothing.
Example:
Input
["MyHashSet", "add", "add", "contains", "contains", "add", "contains", "remove", "contains"]
[[], [1], [2], [1], [3], [2], [2], [2], [2]]
Output
[null, null, null, true, false, null, true, null, false]

Solution:
class MyHashSet {
    ArrayList<Integer> st = new ArrayList<>();
    public MyHashSet() {
        
    }
    
    public void add(int key) {
        st.add(key);
    }
    
    public void remove(int key) {
        if (st.contains(key)) {
            for (int i = 0; i < st.size(); i++) {
                if (st.get(i) == key) {
                    st.remove(i);
                    i--;
                }
            }
        }
    }
    
    public boolean contains(int key) {
        if (st.contains(key)) {
            return true;
        }
        return false;
    }
}


Question 2
LEETCODE 596. Classes More Than 5 Students
Table: Courses
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| student     | varchar |
| class       | varchar |
+-------------+---------+
(student, class) is the primary key (combination of columns with unique values) for this table.
Each row of this table indicates the name of a student and the class in which they are enrolled.
Write a solution to find all the classes that have at least five students.
Return the result table in any order.
The result format is in the following example.
Example 1:
Input: 
Courses table:
+---------+----------+
| student | class    |
+---------+----------+
| A       | Math     |
| B       | English  |
| C       | Math     |
| D       | Biology  |
| E       | Math     |
| F       | Computer |
| G       | Math     |
| H       | Math     |
| I       | Math     |
+---------+----------+
Output: 
+---------+
| class   |
+---------+
| Math    |
+---------+
Explanation: 
- Math has 6 students, so we include it.
- English has 1 student, so we do not include it.
- Biology has 1 student, so we do not include it.
- Computer has 1 student, so we do not include it.

Solution
select class 
from Courses
group by class
having count(student) >= 5;

Question 3
LEETCODE 1877. Minimize Maximum Pair Sum in Array
The pair sum of a pair (a,b) is equal to a + b. The maximum pair sum is the largest pair sum in a list of pairs.
For example, if we have pairs (1,5), (2,3), and (4,4), the maximum pair sum would be max(1+5, 2+3, 4+4) = max(6, 5, 8) = 8.
Given an array nums of even length n, pair up the elements of nums into n / 2 pairs such that:
Each element of nums is in exactly one pair, and
The maximum pair sum is minimized.
Return the minimized maximum pair sum after optimally pairing up the elements.
Example 1:
Input: nums = [3,5,2,3]
Output: 7
Explanation: The elements can be paired up into pairs (3,3) and (5,2).
The maximum pair sum is max(3+3, 5+2) = max(6, 7) = 7.

Solution
class Solution {
    public int minPairSum(int[] nums) {
        int n = nums.length;
        Arrays.sort(nums);
        int max = 0;
        for (int i = 0; i < n / 2; i++) {
            int sum = nums[i] + nums[n - i - 1];
            max = Math.max(sum, max);
        }
        return max;
    }
}

Question 4
LEETCODE 137. Single Number II
Given an integer array nums where every element appears three times except for one, which appears exactly once. Find the single element and return it.
You must implement a solution with a linear runtime complexity and use only constant extra space.
Example 1:
Input: nums = [2,2,3,2]
Output: 3

Solution
class Solution {
    public int singleNumber(int[] nums) {
        if (nums.length == 1) {
            return nums[0];
        }
        Arrays.sort(nums);
        int l = 0;
        for(int i = 0; i <nums.length - 1; i++) {
            if( nums[i]==nums[i+1] ) {
                i = i+2;
            } else {
                l = nums[i];
            }
        }

        if (nums[nums.length - 1] != nums[nums.length - 2]) {
            l = nums[nums.length - 1];
        }
        return l;
    }
}

Question 5 
LEETCODE 46. Permutations
Given an array nums of distinct integers, return all the possible 
permutations. You can return the answer in any order.
Example 1:
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

Solution
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        solve (nums, 0, ans);
        return ans;
    }

    public void solve (int[] nums, int ind, List<List<Integer>> ans) {
        if (ind >= nums.length) {
            List<Integer> arr = new ArrayList<>();
            for (int i = 0; i < nums.length; i++) {
                arr.add(nums[i]);
            }
            ans.add(arr);
            return;
        }
        for (int i = ind; i < nums.length; i++) {

            swap (nums, ind, i);
            solve (nums, ind + 1, ans);
            swap (nums, i, ind);
        }
        
    }
    public void swap (int[] nums, int ind, int i)
    {
        int temp = nums[ind];
        nums[ind] = nums[i];
        nums[i] = temp;
    }
}