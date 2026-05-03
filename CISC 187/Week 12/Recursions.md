# Recursions

## Task 1
Base case:
```cpp
return if low > high
```

## Task 2
If we run factorial(10) using this function, the function will never reach the base case (n == 1) because it subtracts 2 each time. Starting from 10, it goes to 8, 6, 4, 2, 0, then negative numbers. Since n will never equal 1, the recursion continues indefinitely, eventually causing a stack overflow.

## Task 3
```cpp
def sum(low, high)
  return low if low == high
  return high + sum(low, high - 1)
end
```

## Task 4
```cpp
def print_numbers(array)
  array.each do |item|
    if item.is_a?(Array)
      print_numbers(item)
    else
      puts item
    end
  end
end
```
