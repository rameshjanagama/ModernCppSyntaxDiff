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
* [LAMDA]
  * [lamda-notes](#lamda-notes)
* [BIND to LAMDA](#bind)
  * [bind to lambda](#bind-lamda)   
* [Template MetaProgamming](#tmp)
  * [type_traits](#type-traits)      
* [Concepts](#concepts)
  * [C++20](#Concepts2)   
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

for (it = myMap.begin(); it != myMap.end(); it++)
{
    std::cout << it->first << ':' << it->second << std::endl;
}
```
**C++11**

```
for (auto const& x : myMap)
{
    std::cout << x.first << ':' << x.second << std::endl;
}
```
**C++17**

```
for (auto const& [key, val] : myMap)
{
    std::cout << key << ':' << val << std::endl;
}
```
# LAMDA

## lamda-notes
1. What you can’t do prior to C++11 is to create small function on the fly which can use variables from the containing scope and pass it as parameter to another function. 
2. C++11 lamda expression enables you to create functions without name and with data binding, store it, create copy of it, pass as parameter to a function and return from a function. All this property makes lamda as first class function or closer.

**C++11**
**C++14**
**C++17**
**C++20**
**C++23**

# BIND

## bind-lamda


**C++11**
std::bind
```
struct foo
{
  typedef void result_type;

  template < typename A, typename B >
  void operator()(A a, B b)
  {
    cout << a << ' ' << b;
  }
};

auto f = bind(foo(), _1, _2);
f( "test", 1.2f ); // will print "test 1.2"
```
1. You can't move the variables while capturing when creating the lambdas. Variables are always captured as lvalues. For bind you can write:

```
auto f1 = std::bind(f, 42, _1, std::move(v));
```
2. Expressions can't be captured, only identifiers can. For bind you can write:

```
auto f1 = std::bind(f, 42, _1, a + b);
```

3. Overloading arguments for function objects. 
4. Impossible to perfect-forward arguments

**C++14**
lambda
```
auto f = []( auto a, auto b ){ cout << a << ' ' << b; }
f( "test", 1.2f ); // will print "test 1.2"
```

1.Move example:
```
auto f1 = [v = std::move(v)](auto arg) { f(42, arg, std::move(v)); };
```
2. Expression example:
```
auto f1 = [sum = a + b](auto arg) { f(42, arg, sum); };
```
4. Perfect forwarding: You can write
```
auto f1 = [=](auto&& arg) { f(42, std::forward<decltype(arg)>(arg)); };
```

# TMP

## type-traits

## different syntaxes of enable_if

C++11:
```
template<typename T>
typename std::enable_if<(sizeof(T) > 4)>::type
foo() {
}
```

C++14: removed type and typename 
```
template<typename T>
std::enable_if_t<(sizeof(T) > 4)>
foo() {
}
```

OR as last argument of template
```
template<typename T,
         typename = std::enable_if_t<(sizeof(T) > 4)>>
void foo() {
}
```
OR using template aliase(note separate template for alias)
```
template<typename T>
using EnableIfSizeGreater4 = std::enable_if_t<(sizeof(T) > 4)>;

template<typename T,
         typename = EnableIfSizeGreater4<T>>
void foo() {
}
```

# concepts

## Concepts2

```
template<typename STR>
requires std::is_convertible_v<STR,std::string>
Person(STR&& n) : name(std::forward<STR>(n)) {
    …
}
```
OR 
```
template<typename T>
concept ConvertibleToString = std::is_convertible_v<T,std::string>;

template<typename STR>
requires ConvertibleToString<STR>
Person(STR&& n) : name(std::forward<STR>(n)) {
    …
}
```



```
