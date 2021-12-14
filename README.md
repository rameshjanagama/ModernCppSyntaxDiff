# Modern C++ Syntax Diff

Modern C++ - Syntax Difference between various standards of C++. 

Note: please update new differences or correct if any mistakes.

<!-- md-cpp-begin -->
# Table of Content
* [SET](#set)
  * [set insertion](#set-insertion)
* [VECTOR](#vector)
  * [vector find](#vector-find)
* [MAP](#map)
  * [map iteration](#map-iteration)   
<!-- md-cpp-end -->

# SET

## set insertion

**Before C++17**
```
std::set<int> mySet;
set::set<int>::iterator iter;
bool inserted { false };
std::tie(iter, inserted) = mySet.insert(55);
```
**C++17**
```
std::set<int> mySet;
auto [iter, inserted ] = mySet.insert(55);
```

# VECTOR

## vector find

**Before C++17**
```
// Find and replace abc with $$$
const auto it = find(begin(str), end(str), "abc");
 
if (it != end(str)) {
   *it = "$$$";
}
```
**C++17**
```
if (const auto it =  find(begin(str), end(str), "abc");
    it != end(str)) {
    *it = "$$$";
}
```

# MAP

## map iteration

**Before C++11**
```
map<string, int>::iterator it;

for (it = symbolTable.begin(); it != symbolTable.end(); it++)
{
    std::cout << it->first << ':' << it->second << std::endl;
}
```
**C++11**

```
for (auto const& x : symbolTable)
{
    std::cout << x.first << ':' << x.second << std::endl;
}
```
**C++17**

```
for (auto const& [key, val] : symbolTable)
{
    std::cout << key << ':' << val << std::endl;
}
```
