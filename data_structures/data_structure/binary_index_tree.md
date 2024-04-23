# Binary Index Tree
## 定义
A Fenwick tree or binary indexed tree is a data structure that can efficiently update elements and calculate prefix sums in a table of numbers.

<img src="../assets/binary_index_tree.png" width="400" />

## method
- update(): update binary index tree 
- getSum():

## Implementation
```c++
using namespace std;

class BITree {
public:
    vector<int> BITree;

    BITree(n, vector<int>& arr){
        BITree.resize(n+1)
    
        // Store the actual values in BITree[] using update()
        for (int i = 0; i < n; i++)
            updateBIT(i, arr[i]);
    }
    
    int getSum(int index)
    {
        int sum = 0; // Initialize result
    
        // index in BITree[] is 1 more than the index in arr[]
        index = index + 1;
    
        // Traverse ancestors of BITree[index]
        while (index > 0)
        {
            // Add current element of BITree to sum
            sum += this.BITree[index];
    
            // Move index to parent node in getSum View
            index -= index & (-index);
        }
        return sum;
    }

    void updateBIT(int index, int val)
    {
        // index in BITree[] is 1 more than the index in arr[]
        index = index + 1;
    
        // Traverse all ancestors and add 'val'
        while (index < this.BItree.size())
        {
            // Add 'val' to current node of BI Tree
            BITree[index] += val;
        
            // Update index to that of parent in update View
            index += index & (-index);
        }
    }
};

// Driver program to test above functions
int main()
{
    int freq[] = {2, 1, 1, 3, 2, 3, 4, 5, 6, 7, 8, 9};
 
    return 0;
}
```