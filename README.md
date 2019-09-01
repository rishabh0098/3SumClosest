# 3SumClosest

## Problem Description
Given an array `nums` of *n* integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.

### Example
`Given array nums = [-1, 2, 1,  4], and target = 1.
The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).`

## Solution
### Two Pointer Approach
We have the following -   
Three integers `x, y, z` such that `x + y + z = sum` and our goal is to minimize `|target - sum|`.  

Let's say we fix one integer `x`, Then, `y + z = sum - x`.  

Now, the closest thing to the `target` would be the target itself. So, we want our `sum` to be almost equal to the target, so that the difference is minimized.  

Since, we have fixed one integer `x`, so, we have `y + z = sum - x = target - x`.  

If we sort the array, then we can easily find the sum of two integers equal to a given value using two-pointer approach.  

We will maintain two pointers, `left` at the start of the array and `right` at the end of array. We will also maintain `mindiff` and `sum` integers to keep track of the minimum difference and the corresponding sum.  

If the sum of the values at these two positions with x is:  
* Equal to `target`, then return the sum `x + y + z`.  
* Less than `target`, then increment left pointer by one.  
* Greater than `target`, then decrement right pointer by one.  

For less than and greater than cases we also, check if the difference b/w `target` and `sum` is less than `mindiff`, if so, we update `sum` and `mindiff`.  

Finally, we return `sum`.  

### Time Complexity
- Sorting an array is done in `O(n log n)` time.
- We are then fixing the first element `x` of the triplet in the outer loop running over all the elements. 
- In the inner loop, we find a pair with `sum` equals `target - x`, using two-pointer approach.

Thus, overall time complexity = `O(nlogn + n^2)` = `O(n^2)`

### Code
#### Java -
```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int mindiff=Integer.MAX_VALUE, sum=0;
        for(int i=0;i<nums.length;i++){
            int left=i+1,right=nums.length-1;
            while(left<right){
                if(nums[left]+nums[right]+nums[i]==target){
                    return target;
                }
                else if(nums[left]+nums[right]+nums[i]>target){
                    if(Math.abs(nums[left]+nums[right]+nums[i]-target) < mindiff){
                        mindiff = Math.abs(nums[left]+nums[right]+nums[i]-target);
                        sum = nums[left]+nums[right]+nums[i];
                    }
                    right--;
                }
                else{
                    if(Math.abs(nums[left]+nums[right]+nums[i]-target) < mindiff){
                        mindiff = Math.abs(nums[left]+nums[right]+nums[i]-target);
                        sum = nums[left]+nums[right]+nums[i];
                    }
                    left++;
                }
            }
        }
        return sum;
    }
}
```
