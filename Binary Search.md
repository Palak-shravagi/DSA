
Nth root of integer
```
class Solution{
	public:
	int NthRoot(int n, int m)
	{
	   long long low = 1, high = m;
	   while(high >= low){
	       long long mid =  (low+high)/2;
	       if(pow(mid,n) == m)return mid;
	       else if(pow(mid,n)>m)high =  mid -1;
	       else low = mid + 1;
	   }
	   return -1;
	}  
};
```
Median of sorted matrix
```
int countSmallerThanMid(vector<int> &row, int mid)
{
  int l = 0, h = row.size() - 1;
  while (l <= h)
  {
    int md = (l + h) >> 1;
    if (row[md] <= mid)
    {
      l = md + 1;
    }
    else
    {
      h = md - 1;
    }
  }
  return l;
}

int Solution::findMedian(vector<vector<int> > &A) {
   int low = 1;
  int high = 1e9;
  int n = A.size();
  int m = A[0].size();
  while (low <= high)
  {
    int mid = (low + high) >> 1;
    int cnt = 0;
    for (int i = 0; i < n; i++)
    {
      cnt += countSmallerThanMid(A[i], mid);
    }
    if (cnt <= (n * m) / 2)
      low = mid + 1;
    else
      high = mid - 1;
  }
  return low;
}

```
Single element in sorted array
```
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        int low = 0;
        int high = nums.size()-2;
        while(low<=high){
            int mid  =  (low + high) >> 1;
            if(nums[mid] ==  nums[mid^1])
                low =  mid + 1;
            // right half
            else 
                high =  mid - 1;
            // left half;
        }
        return nums[low];
    }
};
```
