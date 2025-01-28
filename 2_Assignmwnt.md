OOP Question

Question 1
LEETCODE 1845. Seat Reservation Manager
Design a system that manages the reservation state of n seats that are numbered from 1 to n.
Implement the SeatManager class:
SeatManager(int n) Initializes a SeatManager object that will manage n seats numbered from 1 to n. All seats are initially available.
int reserve() Fetches the smallest-numbered unreserved seat, reserves it, and returns its number.
void unreserve(int seatNumber) Unreserves the seat with the given seatNumber.

Example 1:
Input
["SeatManager", "reserve", "reserve", "unreserve", "reserve", "reserve", "reserve", "reserve", "unreserve"]
[[5], [], [], [2], [], [], [], [], [5]]
Output
[null, 1, 2, null, 2, 3, 4, 5, null]

Solution

class SeatManager {
    int last = 0;
    PriorityQueue<Integer> pq;
    public SeatManager(int n) {
        this.last = 0;
        this.pq = new PriorityQueue<>();    
    }
    
    public int reserve() {
        if (pq.isEmpty()) {
            last++;
            return last;
        } else {
            return pq.poll();
        }
    }
    
    public void unreserve(int seatNumber) {
        if (seatNumber == last) {
            last--;
        } else {
            pq.offer(seatNumber);
        }
    }
}

DBMS Question

Question 2
LEETCODE 586. Customer Placing the Largest Number of Orders
Table: Orders

+-----------------+----------+
| Column Name     | Type     |
+-----------------+----------+
| order_number    | int      |
| customer_number | int      |
+-----------------+----------+
order_number is the primary key (column with unique values) for this table.
This table contains information about the order ID and the customer ID.
Write a solution to find the customer_number for the customer who has placed the largest number of orders.
The test cases are generated so that exactly one customer will have placed more orders than any other customer.
The result format is in the following example.
Example 1:
Input: 
Orders table:
+--------------+-----------------+
| order_number | customer_number |
+--------------+-----------------+
| 1            | 1               |
| 2            | 2               |
| 3            | 3               |
| 4            | 3               |
+--------------+-----------------+
Output: 
+-----------------+
| customer_number |
+-----------------+
| 3               |
+-----------------+
Explanation: 
The customer with number 3 has two orders, which is greater than either customer 1 or 2 because each of them only has one order. 
So the result is customer_number 3.

Solution

select customer_number
from Orders
group by customer_number 
order by count(order_number) 
desc 
limit 1;

DSA Question

Question 3
LEETCODE 94: Given the root of a binary tree, return the inorder traversal of its nodes' values.
Example 1:
Input: root = [1,null,2,3]
Output: [1,3,2]

Solution

class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        ArrayList<Integer> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }
        ans.addAll(inorderTraversal(root.left));
        ans.add(root.val);
        ans.addAll(inorderTraversal(root.right));
        return ans;
    }
}

Question 4
LEETCODE 2683. Neighboring Bitwise XOR
A 0-indexed array derived with length n is derived by computing the bitwise XOR (⊕) of adjacent values in a binary array original of length n.
Specifically, for each index i in the range [0, n - 1]:
If i = n - 1, then derived[i] = original[i] ⊕ original[0].
Otherwise, derived[i] = original[i] ⊕ original[i + 1].
Given an array derived, your task is to determine whether there exists a valid binary array original that could have formed derived.
Return true if such an array exists or false otherwise.
A binary array is an array containing only 0's and 1's
Example 1:
Input: derived = [1,1,0]
Output: true
Explanation: A valid original array that gives derived is [0,1,0].
derived[0] = original[0] ⊕ original[1] = 0 ⊕ 1 = 1 
derived[1] = original[1] ⊕ original[2] = 1 ⊕ 0 = 1
derived[2] = original[2] ⊕ original[0] = 0 ⊕ 0 = 0

Solution
class Solution {
    public boolean doesValidArrayExist(int[] derived) {
        int sum = 0;
        int xor = 0;
        for (int i = 0; i < derived.length; i++) {
            xor ^= derived[i];
            
        }
        return xor == 0;
    }
}

Question 5
LEETCODE 3099. Harshad Number
An integer divisible by the sum of its digits is said to be a Harshad number. You are given an integer x. Return the sum of the digits of x if x is a Harshad number, otherwise, return -1.
Example 1:
Input: x = 18
Output: 9
Explanation:
The sum of digits of x is 9. 18 is divisible by 9. So 18 is a Harshad number and the answer is 9.

Solution
class Solution {
    public int sumOfTheDigitsOfHarshadNumber(int x) {
        int num = x;
        int sum = 0;
        while (num > 0) {
            int rem = num % 10;
            sum += rem;
            num = num / 10;
        }
        return (x % sum == 0) ? sum : -1;
    }
}