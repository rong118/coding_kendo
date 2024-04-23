# Tree Map
##
TreeMap is implemented based on red-black tree structure, and it is ordered by the key.

```c
// c++ Implementation
#include <iostream>;
#include <map>;


int main(){
  std::map<int,int> m;
  m[1] = 10;
  m[2] = 20;
  m[3] = 30;
  auto itlow = m.lower_bound(1);    //point to key 1
  auto itupper = m.upper_bound(2);  //point to key 3
  auto ret = m.equal_range(2);  // ?

  return 0;
}
```

```go
// go 

```
