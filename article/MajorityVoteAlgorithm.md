# Majority Vote Algorithm

The Boyer-Moore majority vote algorithm is to find the majority element in an array using linear time and constant space. The majority element should appear more than n/2 times in an anrray of size n.


## Algorithm
```
Initialize candidate and counter = 0
For each element x in the array:
  if counter = 0
    candidate = x and counter++;
  else if x == candidate
    counter++;
  else
    counter--;
return candidate;
```


## Correctness
When applying the majority vote algorithm on an array, only one of below two cases can happen (Let C be the 1st candidate):
- case 1: counter of C never drops to zero through out the array.
- case 2: counter of C drops to zero at some point.

If case 1, then C is the majority element. If case 2, then there are two sub cases:
- case 2.1: If there exists a majority element M and it has never appeared in the Visited subarray, then it must be the majority of Not-Visited subarray (i.e., variable candidate will hold M at the end). <br/>
- case 2.2: If there exists a majority element M and it has appeared in the Visited subarray. Assuming the array has N elements and Visited has X elements, then M appeared in Visited subarray at most X/2 times. Since total number of M is not less than N/2 + 1, hence the number of M exist in NotVisited subarry is greater than (N/2 + 1) - X/2 = (N - X)/2 + 1. So M is the majority of NotVisited (i.e., variable candidate will hold M at the end).

      |---------Visited---------|---------NotVisited---------|


## Implementation
```C#
public class Solution {
    public int MajorityElement(int[] nums) {
     
        if(nums == null || nums.Length == 0)
            return Int32.MinValue;
        
        int candidate = Int32.MinValue, counter = 0;
        foreach(int num in nums)
        {
            if(counter == 0)
            {
                candidate = num;
                counter++;
            }
            else if(num == candidate)
                counter++;
            else
                counter--;
        }
        
        return candidate;
    }
}
```

### References
1. https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_majority_vote_algorithm
2. https://www.quora.com/What-is-the-proof-of-correctness-of-Moores-voting-algorithm
