# CPP Cheatsheet

## History of C++:

| Standard  | Year | Key Enhancements                                      |
|-----------|------|-------------------------------------------------------|
| **C++98** | 1998 | Initial Standard, Objects, Classes, Inheritance, Templates, Exceptions |
| **C++03** | 2003 | Minor improvements, Fixes for C++98, STL fixes, Namespaces |
| **C++11** | 2011 | Major update, Move Semantics, `auto`, Smart Pointers, Lambda Expressions, Range-based `for` loop |
| **C++14** | 2014 | Features for Convenience, Generic Lambdas, User-defined Literals, `decltype(auto)`, Extended `constexpr` |
| **C++17** | 2017 | Modern Language Features, Folding Expressions, Inline Variables,  `std::filesystem`, `std::optional`, `std::variant`, `std::any` |
| **C++20** | 2020 | Concepts, `requires` clause, Modules, Ranges Library, Coroutines, `consteval`, Feature Test Macros |
| **C++23** | 2023 | `constexpr` Atomics, Extended `std::string_view`, Library Improvements |


## C++98 Quick Reference Guide

The baseline standard that solidified C++ as a distinct language with robust features for object-oriented programming and generic programming. Here's a snapshot of its foundational features:

- **Objects & Classes:** Encapsulation with user-defined types.
- **Inheritance:** Allows derivation of classes for code reusability.
- **Templates:** Enables generic programming, particularly with classes and functions.
- **Exceptions:** Error handling with `try`, `catch`, and `throw`.
- **Namespaces:** Avoids name collisions and organizes code.
- **The C++ Standard Library (STL):** Provides common data structures (vector, map, etc.) and algorithms.
- **Type Casting:** Static, dynamic, const, and reinterpret casts for fine-grained control over type conversion.
- **The `bool` Data Type:** Introduces `true` and `false` as native Boolean values.
- **Function Overloading:** Multiple functions with the same name but different parameters.
- **Operator Overloading:** Custom behavior of operators for custom types.
- **References:** Alias for another variable.
- **Const Qualifier:** Defines immutable entities.
- **Inline Functions:** Optimization feature for smaller functions.
- **`this` Pointer:** Points to the object for which a member function is called.
- **Memory Management:** `new` and `delete` for dynamic allocation.
- **I/O Streams:** Classes for input/output operations (`cin`, `cout`, etc.).
- **File Operations:** File reading/writing with fstream classes.

C++98 established the core language mechanisms that C++ programmers still use today.

### C++98 Examples

- **Objects & Classes:**
  ```cpp
  class Example {
  public:
      int value;
      void doSomething() {}
  };
  ```

- **Inheritance:**
  ```cpp
  class Base { public: void baseFunc() {} };
  class Derived : public Base {};
  ```

- **Templates:**
  ```cpp
  template<typename T>
  T max(T a, T b) { return (a > b) ? a : b; }
  ```

- **Exceptions:**
  ```cpp
  try {
      throw std::runtime_error("Error occurred");
  } catch (const std::exception& e) {
      // Handle exception
  }
  ```

- **Namespaces:**
  ```cpp
  namespace MyNamespace {
      void myFunction() {}
  }
  // Usage: MyNamespace::myFunction();
  ```

- **STL Containers & Algorithms:**
  ```cpp
  #include <vector>
  #include <algorithm>
  std::vector<int> vec = {1, 2, 3};
  std::sort(vec.begin(), vec.end());
  ```

- **Type Casting:**
  ```cpp
  double pi = 3.14;
  int intPi = static_cast<int>(pi);
  ```

- **`bool` Data Type:**
  ```cpp
  bool isSuccess = true;
  ```

- **Function Overloading:**
  ```cpp
  void print(int i) {}
  void print(double f) {}
  ```

- **Operator Overloading:**
  ```cpp
  struct Point {
      int x, y;
      Point operator+(const Point& p) {
          return {x + p.x, y + p.y};
      }
  };
  ```

- **References:**
  ```cpp
  int a = 10;
  int& ref = a;
  ```

- **Const Qualifier:**
  ```cpp
  const int immutableValue = 5;
  ```

- **Inline Functions:**
  ```cpp
  inline int getSquare(int x) { return x * x; }
  ```

- **`this` Pointer:**
  ```cpp
  class SelfRef {
  public:
      SelfRef& returnSelf() { return *this; }
  };
  ```

- **Memory Management:**
  ```cpp
  int* ptr = new int(5);
  delete ptr;
  ```

- **I/O Streams:**
  ```cpp
  std::cout << "Output stream" << std::endl;
  std::cin >> inputValue;
  ```

- **File Operations (fstream):**
  ```cpp
  std::ofstream outfile("file.txt");
  outfile << "File content" << std::endl;
  std::ifstream infile("file.txt");
  std::string content;
  infile >> content;
  ```


## C++03 Changes In Short

- Enhancement and bug-fix release of C++98.

#### Major Features
- Fixes: Addresses defects and ambiguities in C++98.
- Library Improvements: Minor additions and fixes to the Standard Library and STL.
- Value Semantics: Clarified for temporaries and exceptions.

#### Detailed Enhancements
- Improved `std::vector` performance: Exception safety guarantees with `pop_back` and `erase`.
- Optimized `std::string`: Reference counting and copy-on-write deprecation.
- Enhanced `std::allocator`: Addressed memory model issues.
- Added `value_type` and `pointer` types to standard allocators.

#### Keywords
- No new keywords introduced.

#### Miscellaneous
- `export` template (rarely implemented and later removed in C++11): Aims for separate template compilation.
- `std::mem_fun` and `std::not1/not2`: Adaptors for function pointers and negating predicates.

##### std::mem_fun
```cpp
#include <vector>
#include <algorithm>
#include <functional>
#include <iostream>

class Foo {
public:
    void display() { std::cout << "Foo\n"; }
};

int main() {
    std::vector<Foo> foos(3);
    std::for_each(foos.begin(), foos.end(), std::mem_fun_ref(&Foo::display));
}
```
Output:
```
Foo
Foo
Foo
```
##### std::not1
```cpp
#include <algorithm>
#include <vector>
#include <functional>
#include <iostream>

bool isOdd(int n) { return n % 2 == 1; }

int main() {
    std::vector<int> v {1, 2, 3, 4, 5};
    auto it = std::find_if(v.begin(), v.end(), std::not1(std::ptr_fun(isOdd)));
    std::cout << *it << '\n';  // Find the first even number
}
```
Output:
```
2
```


## C++11 Quick Reference Guide

C++11, widely recognized as a major update to the C++ language, introduced a range of features to simplify code, improve performance, and enhance the type system. Here's a concise rundown of the key features:

| Feature                  | Description                                    | Example                                                   |
|--------------------------|------------------------------------------------|-----------------------------------------------------------|
| `auto`                   | Type inference for variables                   | `auto x = 42; // x is int`                                |
| `nullptr`                | Null pointer literal                           | `int* ptr = nullptr;`                                     |
| Uniform initialization   | Consistent initialization for all types        | `std::vector<int> v{1, 2, 3};`                            |
| Initializer lists        | List initialization syntax `{}`                | `std::map<int, std::string> m{{1, "one"}, {2, "two"}};`   |
| `constexpr`              | Compile-time constant expressions              | `constexpr int square(int x) { return x * x; }`           |
| Range-based `for` loop   | Iterate over containers easily                 | `for (auto& e : v) { /* ... */ }`                         |
| Lambda expressions       | Inline anonymous functions                     | `auto sum = [](int x, int y) { return x + y; };`           |
| Move semantics           | Efficient object transfer                      | `std::vector<int> v2 = std::move(v1);`                    |
| Smart pointers           | Automatic resource management                  | `std::unique_ptr<int> p(new int(5));`                     |
| `enum class`             | Scoped and strongly-typed enums                | `enum class Color { red, green, blue };`                  |
| Rvalue references (`&&`) | For move semantics and perfect forwarding      | `void f(int&& x) { /* ... */ }`                           |
| Variadic templates       | Templates with variable number of args         | `template<typename... Args> void f(Args... args);`        |
| `static_assert`          | Compile-time assertions                        | `static_assert(sizeof(int) == 4, "Integers are not 32-bit");` |
| `thread_local`           | Thread-local storage                           | `thread_local int counter = 0;`                           |
| Multithreading support   | Concurrency tools                              | `std::thread t([]{ /* ... */ });`                         |
| New algorithms           | Extended algorithm library                     | `std::copy_n(src.begin(), 3, dest.begin());`              |
| New data structures      | Additional containers and types                | `std::array<int, 3> arr = {1, 2, 3};`                     |
| `decltype`               | Deduction of type from an expression           | `decltype(arr) arr2 = arr; // std::array<int, 3>`         |
| Enhanced STL functional  | Function objects and binders                   | `std::function<int(int)> f = [](int x) { return x * x; };`|
| Attributes               | Compiler hints and optimizations               | `[[nodiscard]] int get_value() { /* ... */ }`             |
| Standardized memory model| Defines memory consistency for concurrency     | *Used implicitly in multithreaded operations*             |
| Trailing return types    | Alternative function syntax                    | `auto f() -> int { return 42; }`                          |


## C++14 Quick Reference Guide

- **Auto Type Deduction**: `decltype(auto)` enables auto deduction in more contexts.
- **Return Type Deduction**: Functions can omit the return type, deduced from `return` expressions.
- **Generic Lambdas**: Template parameters in lambdas allow for auto type in the parameter list.
- **Variable Templates**: Templates now applicable to variables, not just classes and functions.
- **Binary Literals**: Direct binary representation (`0b` or `0B` prefix) for integral literals.
- **Digit Separators**: Single quotes (`'`) improve readability of numeric literals.
- **Relaxed `constexpr`**: `constexpr` functions can now have loops, multiple statements.
- **Sized Deallocation**: Customization point for deallocation functions to use the size of the deallocated block.
- **Aggregate Member Initialization**: Non-static data members initialization using braces.
- **Standard User-Defined Literals**: Additional literals for standard library types (e.g., `s` for `std::string`).
- **Shared Timed Mutex**: Concurrent access allowing timed lock attempts (`std::shared_timed_mutex`).
- **Library Improvements**: Expanded functionality for `std::function`, smarter `std::bind`, etc.

### C++14 Examples

- **Auto Type Deduction**:
```cpp
auto x = 2;        // int
decltype(auto) y = x; // int
```

- **Return Type Deduction**:
```cpp
auto f() { return 7; } // deduces return type as int
```

- **Generic Lambdas**:
```cpp
auto lambda = [](auto x, auto y) { return x + y; };
```

- **Variable Templates**:
```cpp
template <typename T>
constexpr T pi = T(3.1415926535897932385);
```

- **Binary Literals**:
```cpp
auto binary = 0b1010; // 10 in decimal
```

- **Digit Separators**:
```cpp
auto large_number = 1'000'000; // easier to read than 1000000
```

- **Relaxed `constexpr`**:
```cpp
constexpr int factorial(int n) {
    int result = 1;
    for (int i = 1; i <= n; ++i) result *= i;
    return result;
}
```

- **Sized Deallocation**:
```cpp
// Requires a suitable operator delete defined
void operator delete(void* ptr, std::size_t sz) {
    std::cout << "Deallocating " << sz << " bytes\n";
    ::operator delete(ptr);
}
```

- **Aggregate Member Initialization**:
```cpp
struct Point {int x, y;};
Point p{1, 2}; // Aggregate initialization
```

- **Standard User-Defined Literals**:
```cpp
using namespace std::string_literals;
auto text = "Hello"s; // std::string
```

- **Shared Timed Mutex**:
```cpp
std::shared_timed_mutex stm;
stm.try_lock_for(std::chrono::seconds(1)); // Attempts lock, times out after 1 second
```

- **Library Improvements**:
```cpp
std::function<void(int)> fun = [](int x) { std::cout << x; };
std::bind(fun, 42)(); // Calls the lambda with 42
```


## C++17 Quick Reference Guide (with Examples)

**Structured Bindings:**
- Unpack tuple or struct into separate variables.
```cpp
auto [a, b] = make_tuple(1, 'c');
```

**if/switch with Initializers:**
- Initialize variable in `if` and `switch` conditions.
```cpp
if (auto it = map.find(key); it != map.end()) { /* ... */ }
```

**Inline Variables**
- Define `inline` variables in headers, safe for multiple inclusions.
```cpp
inline constexpr int MaxSize = 100;
```

**Folding Expressions:**
- Apply operator to pack of parameters.
```cpp
template<typename... Args>
auto sum(Args... args) { return (... + args); }
```

**std::optional:**
- Wrapper for value that may or may not exist.
```cpp
std::optional<int> maybeInt;
```

**std::variant:**
- Type-safe union.
```cpp
std::variant<int, float> num;
```

**std::any:**
- Store any type.
```cpp
std::any value = 123;
```

**std::filesystem:**
- Portable interface for file system operations.
```cpp
std::filesystem::create_directory("folder");
```

**std::string_view:**
- Non-owning reference to `std::string`.
```cpp
void print(std::string_view sv) { std::cout << sv; }
```

**Hexadecimal Floating-point Literals:**
- Hex representation for floating-points.
```cpp
auto f = 0x1.ep3; // 1.875 * 2^3
```

**New Attributes:**
- `[[nodiscard]]`, `[[maybe_unused]]`, `[[fallthrough]]`
```cpp
[[nodiscard]] int foo();
[[maybe_unused]] static int x = 42;
[[fallthrough]];
```

**Deprecated Attributes:**
- `[deprecated]` attribute to mark entities not recommended for use.
```cpp
[[deprecated("Use newFunction()")]]
void oldFunction() {}
```

**Parallel STL Algorithms:**
- Execute algorithms with parallel execution policies.
```cpp
std::sort(std::execution::par, vec.begin(), vec.end());
```

**Remove and Remove_if for std::(w)string:**
- Easier way to remove characters.
```cpp
std::string str = "text";
str.erase(std::remove(str.begin(), str.end(), 'x'), str.end());
```

**Improved Lambda Expressions:**
- Capture `*this`, and auto return type in generic lambdas.
```cpp
auto lambda = [*this](auto x) { return x; };
```


## C++20 Quick Reference Guide

- **Concepts**: Define template requirements (`concept` keyword).
- **Requires Clauses**: Conditionally compile functions (`requires`).
- **Modules**: Replace header files for faster compilation (`import`, `export`).
- **Ranges**: Composable operations on sequences (`std::ranges`).
- **Coroutines**: Asynchronous programming (`co_await`, `co_return`, `co_yield`).
- **Constexpr**: Expanded usage for constant expressions.
- **Constinit**: Guarantee constant initialization.
- **Lambda Improvements**: Default constructible/copyable, template syntax.
- **Designated Initializers**: `{.member=value}` for aggregates.
- **Template Syntax for Lambdas**: Allows `auto` in parameter list.
- **Three-way Comparison Operator**: `<=>`, aka "spaceship operator".
- **New STL Features**: `std::span`, `std::bit_cast`, `std::starts_with`, `std::ends_with`.
- **Calendars and Time Zones**: `<chrono>` improvements.
- **Feature Test Macros**: Check for compiler features (`__cpp_lib_ranges`).
- **`std::format`**: Text formatting simliar to `fmtlib`.
- **`consteval`**: Functions that are always evaluated at compile-time.
- **`std::source_location`**: Access information about the source code location.
- **`std::is_constant_evaluated`**: Check if in constant evaluation context.


### C++20 Examples

- **Concepts**: Define template requirements.
  ```cpp
  template<typename T>
  concept Integral = std::is_integral_v<T>;

  template<Integral T>
  T add(T a, T b) { return a + b; }
  ```

- **Requires Clauses**: Function overloading based on constraints.
  ```cpp
  template<typename T>
  requires std::is_integral_v<T>
  T multiply(T a, T b) { return a * b; }
  ```

- **Modules**: Organize code into modules.
  ```cpp
  // mymodule.cpp
  export module mymodule;
  export int add(int a, int b) { return a + b; }

  // main.cpp
  import mymodule;
  int sum = add(3, 4);
  ```

- **Ranges**: Composable operations on sequences.
  ```cpp
  #include <ranges>
  std::vector<int> v = {1, 2, 3, 4};
  auto even = v | std::views::filter([](int i){ return i % 2 == 0;});
  ```

- **Coroutines**: Asynchronous operations.
  ```cpp
  std::future<int> async_function() {
    co_return 42; // Resumes when handling the future
  }
  ```

- **Constexpr**: Expanded usage.
  ```cpp
  constexpr std::array<int, 3> arr = {1, 2, 3};
  ```

- **Constinit**: Ensure constant initialization.
  ```cpp
  constinit int myGlobalConst = 10;
  ```

- **Lambda Improvements**: Simplified creation and use of lambdas.
  ```cpp
  auto lambda = []<typename T>(T a, T b) { return a < b; };
  ```

- **Designated Initializers**: Aggregate initialization.
  ```cpp
  struct Point { int x; int y; };
  Point p = {.x = 10, .y = 20};
  ```

- **Three-way Comparison Operator**: Simplified comparisons.
  ```cpp
  auto result = (a <=> b) < 0;
  ```

- **New STL Features**: New Standard Library functionalities.
  ```cpp
  std::span<int> mySpan(arr);
  ```

- **Calendars and Time Zones**: Time handling improvements.
  ```cpp
  using namespace std::chrono;
  auto now = zoned_time{current_zone(), system_clock::now()};
  ```

- **Feature Test Macros**: Check for available features.
  ```cpp
  #if defined(__cpp_lib_ranges)
    // Use std::ranges
  #endif
  ```

- **`std::format`**: Advanced formatting.
  ```cpp
  std::string s = std::format("Hello, {}!", "world");
  ```

- **`consteval`**: Ensure expressions are evaluated at compile-time.
  ```cpp
  consteval int sqr(int n) { return n * n; }
  constexpr auto squared = sqr(10);
  ```

- **`std::source_location`**: Retrieve information about source code.
  ```cpp
  void log(const std::source_location& location = std::source_location::current()) {
    std::cout << "file: " << location.file_name() << " line: " << location.line();
  }
  ```

- **`std::is_constant_evaluated`**: Optimize for compile-time evaluation.
  ```cpp
  constexpr bool inConstexpr = std::is_constant_evaluated();
  ```


## C++23 Quick Reference Guide

**Language Features:**
- `constexpr` Function Enhancements: Broader use, including dynamic allocation and `std::vector`.
- `if consteval`: Conditional compilation depending on whether context is `constexpr`.
- `constinit if`: Static if-initialization.
- `auto(x)`: New placeholder syntax for `decltype(auto)`.

**Library Updates:**
- `std::expected<T, E>`: Error handling construct, representing a value or an error.
- `std::stacktrace`: Utilities for capturing and printing stack traces.
- `std::mdspan`: Multi-dimensional view for data arrays (non-owning).
- `std::ranges::to`: Converts ranges to containers like `std::vector`.
- `std::flat_map` & `std::flat_set`: Sorted vector-based associative containers.
- `std::basic_string::resize_and_overwrite`: Efficiently resize and populate `std::string`.
- `std::print`: For formatted output, an alternative to `printf`.

**Concurrency & Parallelism:**
- Improvements to `std::jthread` and `std::stop_token`.

**Utilities:**
- `std::ssize()`: Signed size function for containers.
- `std::osyncstream`: Synced output stream for multi-threaded environment.

**Compiler Support:**
- Compiler introspection features via attributes like `[[nodiscard("reason")]]`.
- New C++ standard attribute `[[nodiscard]]` for constructors.
- `[[assert]]` and `[[expects]]` attributes for pre-conditions in code.

**Miscellaneous:**
- Portability and consistency improvements.
- Extended `constexpr` and `noexcept` applicability.
- More `[[deprecate]]` options for smoother API transitions.


### C++23 Examples

**Language Features:**
- `constexpr` Enhancements:
```cpp
constexpr std::vector<int> make_vector() {
  std::vector<int> v = {1, 2, 3};
  return v;
}
auto v = make_vector(); // Now valid in C++23
```

- `if consteval`:
```cpp
void foo() {
  if consteval {
    // Compile-time branch
  } else {
    // Run-time branch
  }
}
```

- `constinit if`:
```cpp
constinit if (std::is_constant_evaluated()) {
  // Static if-initialization
}
```

- Auto type deduction (`decltype(auto)`) using `auto(x)`:
```cpp
int a = 42;
auto(&x) = a; // x has type int&
```

**Library Updates:**
- `std::expected<T, E>`:
```cpp
std::expected<int, std::string> getResult() {
  if (/* success condition */) return 42;
  else return std::unexpected<std::string>("Error");
}
```

- `std::stacktrace`:
```cpp
void print_stacktrace() {
  std::cout << std::stacktrace::current();
}
```

- `std::mdspan`:
```cpp
std::vector<double> data(24);
auto mdspan_view = std::mdspan<double, std::extents<4, 3, 2>>(data.data());
```

- `std::ranges::to`:
```cpp
auto vec = std::ranges::iota_view(0, 10) | std::ranges::to<std::vector>();
```

- `std::flat_map` & `std::flat_set`:
```cpp
std::flat_map<int, std::string> fmap = {{1, "one"}, {2, "two"}};
std::flat_set<int> fset = {1, 2, 3};
```

- `std::basic_string::resize_and_overwrite`:
```cpp
std::string s;
s.resize_and_overwrite(100, [](char* ptr, std::size_t size) {
  // Fill ptr here, return new size
  return size;
});
```

- `std::print`:
```cpp
std::print("Hello, {}!", "World");
```

**Concurrency & Parallelism:**
- `std::jthread` and `std::stop_token` Improvements:
```cpp
std::jthread t([](std::stop_token stop_token) {
  while (!stop_token.stop_requested()) {
    // Do work unless stop is requested
  }
});
t.request_stop(); // Stops the thread once the current work is done
```

**Utilities:**
- `std::ssize()`:
```cpp
std::vector<int> vec = {1, 2, 3};
auto size = std::ssize(vec); // Signed size
```

- `std::osyncstream`:
```cpp
std::osyncstream out(std::cout);
out << "Thread-safe output to cout\n";
```

**Compiler Support:**
- `[[nodiscard("reason")]]`:
```cpp
[[nodiscard("Returning an error state")]]
int get_data() { /* ... */ }
```

- `[[nodiscard]]` for constructors:
```cpp
struct [[nodiscard]] S {
  S();
};

S createS() { return S(); }

void useS() {
  createS(); // Warning: nodiscard type S is discarded
}
```

- `[[assert]]` and `[[expects]]`:
```cpp
int foo(int x) [[expects: x > 0]] [[assert: x < 100]] {
  return x;
}
```

**Miscellaneous:**
- Deprecation:
```cpp
[[deprecated("Use new_func() instead")]]
void old_func() {
  // ...
}
```
