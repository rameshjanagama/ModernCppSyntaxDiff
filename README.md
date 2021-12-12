# Modern C+++ Syntax Diff
Modern C++ -  Syntax Difference

# Tuples or Pair 
## C++11 
###### C++11 
code:

```
std::set<int> mySet;
set::set<int>::iterator iter;
bool inserted { false };
std::tie(iter, inserted) = mySet.insert(55);
```
###### TC++17 
## C++17
###### TC++17
code:

```
std::set<int> mySet;
auto [iter, inserted ] = mySet.insert(55);
```



