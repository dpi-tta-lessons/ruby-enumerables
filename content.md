# Enumerables
Now that we understand how to use loops and the each method to iterate through arrays and other collections, let’s dive into the powerful world of Enumerables. [Enumerables](https://ruby-doc.org/3.2.2/Enumerable.html) are a set of methods that allow us to traverse, search, sort, and manipulate collections in Ruby. They provide a more expressive and readable way to handle collections compared to basic loops and make code easier to understand and maintain.

Let’s look at some of the most common Enumerable methods and how they can simplify our code.

## `each` method recap
As we’ve already seen, the each method is one of the simplest ways to iterate over a collection:

```ruby
numbers = [1, 2, 3, 4, 5]

numbers.each do |number|
  pp number
end
```
{: .repl #each_recap title="each method recap" points="1"}

Here, `each` iterates through each element in the numbers array and prints it. This method is great for performing actions on each element, but what if we want to create a new collection based on the values from another?

## `map` method
The map method (also known as collect) transforms each element of a collection according to the block provided and returns a new array of transformed elements:

```ruby
numbers = [1, 2, 3, 4, 5]

squares = numbers.map do |number|
  number * number
end

pp squares
```
{: .repl #map_example title="map method" points="1"}

In this example, we use `map` to create a new array, squares, containing the squares of each number in the original numbers array. `map` is perfect when you need to transform data from one form to another.

### Practice using `map`
Write a program that takes a randomly sampled words array, converts each word to uppercase, and stores the results in a new array. Print the new array.

For example, if `words = ["apple", "banana", "cherry"]`, the output should be `["APPLE", "BANANA", "CHERRY"]`

```ruby
words = ["ruby", "python", "java"].sample(2)
# write your program here
```
{: .repl #map_practice title="map practice" readonly_lines="[1]" points="1"}

```ruby
describe "Map practice" do
  it "should print 'APPLE', 'BANANA', 'CHERRY' if the input is ['apple', 'banana', 'cherry']" do
    path = "/tmp/code.rb"

    file = File.read(path)
    new_content = file.split("\n")
    new_content = new_content.map { |line| line == 'words = ["ruby", "python", "java"].sample(2)' ? 'words = ["apple", "banana", "cherry"]' : line }.join("\n")
    File.open(path, 'w') { |line| line.puts new_content }

    expect { require_relative(path) }.to output("[\"APPLE\", \"BANANA\", \"CHERRY\"]\n").to_stdout
  end
end
```
{: .repl-test #map_practice_test_1 for="map_practice" title="Map practice should print 'APPLE', 'BANANA', 'CHERRY' if the input is ['apple', 'banana', 'cherry']" points="1"}

## `select` and `reject` methods
Sometimes we want to filter elements in a collection based on certain criteria. This is where `select` (also known as `filter`) and `reject` come in handy.

- `select` returns a new array containing all elements for which the block returns true.
- `reject` returns a new array containing all elements for which the block returns false.

Let's look at examples for each:

```ruby
numbers = [1, 2, 3, 4, 5]

even_numbers = numbers.select do |number|
  number.even?
end

pp even_numbers
```
{: .repl #select_example title="select method" points="1"}

```ruby
numbers = [1, 2, 3, 4, 5]

odd_numbers = numbers.reject do |number|
  number.even?
end

pp odd_numbers
```
{: .repl #reject_example title="reject method" points="1"}

### Practice using select and reject
Write a program that takes a randomly sampled numbers array and separates the even and odd numbers into two different arrays using select and reject. Print both arrays.

For example, if `numbers = [1, 2, 3, 4, 5, 6]`, the output should be:

```ruby
[2, 4, 6]
[1, 3, 5]
```

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9].sample(6)
# write your program here
```
{: .repl #select_reject_practice title="select and reject practice" readonly_lines="[1]" points="1"}

```ruby
describe "Select and Reject practice" do
  it "should print '[2, 4, 6]' and '[1, 3, 5]' if the input is [1, 2, 3, 4, 5, 6]" do
    path = "/tmp/code.rb"

    file = File.read(path)
    new_content = file.split("\n")
    new_content = new_content.map { |line| line == 'numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9].sample(6)' ? 'numbers = [1, 2, 3, 4, 5, 6]' : line }.join("\n")
    File.open(path, 'w') { |line| line.puts new_content }

    expect { require_relative(path) }.to output("[2, 4, 6]\n[1, 3, 5]\n").to_stdout
  end
end
```
{: .repl-test #select_reject_practice_test_1 for="select_reject_practice" title="Select and Reject practice should print '[2, 4, 6]' and '[1, 3, 5]' if the input is [1, 2, 3, 4, 5, 6]" points="1"}

## `find` and `find_all` methods
Another common task is searching for elements. The find (also known as detect) method returns the first element for which the block returns true. The find_all method returns all elements for which the block returns true.

Here's how they work:

```ruby
numbers = [1, 2, 3, 4, 5]

first_even = numbers.find do |number|
  number.even?
end

pp first_even
```
{: .repl #find_example title="find method" points="1"}

```ruby
numbers = [1, 2, 3, 4, 5]

all_even = numbers.find_all do |number|
  number.even?
end

pp all_even
```
{: .repl #find_all_example title="find_all method" points="1"}

### Practice using `find` and `find_all`
Write a program that takes a randomly sampled numbers array and finds the first even number using `find` and all odd numbers using `find_all`. Print both results.

For example, if numbers = [1, 3, 5, 2, 4], the output should be:

```ruby
2
[1, 3, 5]
```

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9].shuffle
# write your program here
```
{: .repl #find_find_all_practice title="find and find_all practice" readonly_lines="[1]" points="1"}

```ruby
describe "Find and Find_all practice" do
  it "should print '2' and '[1, 3, 5]' if the input is [1, 3, 5, 2, 4]" do
    path = "/tmp/code.rb"

    file = File.read(path)
    new_content = file.split("\n")
    new_content = new_content.map { |line| line == 'numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9].shuffle' ? 'numbers = [1, 3, 5, 2, 4]' : line }.join("\n")
    File.open(path, 'w') { |line| line.puts new_content }

    expect { require_relative(path) }.to output("2\n[1, 3, 5]\n").to_stdout
  end
end
```
{: .repl-test #find_find_all_practice_test_1 for="find_find_all_practice" title="Find and Find_all practice should print '2' and '[1, 3, 5]' if the input is [1, 3, 5, 2, 4]" points="1"}

## `do...end` vs `{}` vs `&` Block Syntax in Ruby Enumerables
In Ruby, there are three common syntaxes for writing blocks of code: `do...end`, `{}`, and `&`. These syntaxes are used to define blocks, but there are subtle differences in how and when to use each.

### `do...end` Block Syntax
The do...end syntax is often used for multi-line blocks. It is more readable for longer blocks of code and is commonly used when the block performs a series of operations.

```ruby
numbers = [1, 2, 3, 4, 5]

numbers.each do |number|
  pp number * number
  pp number + 1
end
```
{: .repl #do_end_example title="do...end block" points="1"}

### `{}` Block Syntax
The `{}` curly braces syntax is typically used for single-line blocks. It is more concise and is often used when the block contains only one line of code or when a method call is embedded within another expression.

```ruby
numbers = [1, 2, 3, 4, 5]

squares = numbers.map { |number| number * number }

pp squares
```
{: .repl #curly_braces_example title="Curly braces block" points="1"}

### Using the `&` Shorthand with Enumerable Methods
The `&` shorthand is a way to convert a symbol representing a method name into a block that calls that method on each element of the collection. This shorthand can be used with any method that takes a block, such as `map`, `select`, `reject`, and others.

For example, consider the following code that uses `map` to convert an array of strings to uppercase:

```ruby
words = ["hello", "world", "ruby"]

upcased_words = words.map { |word| word.upcase }

pp upcased_words
```
{: .repl #map_upcase_example title="map with block" points="1"}

This code can be made more concise using the `&` shorthand:

```ruby
words = ["hello", "world", "ruby"]

upcased_words = words.map(&:upcase)

pp upcased_words
```
{: .repl #map_upcase_shorthand title="map with & shorthand" points="1"}

### Combining `do...end`, `{}`, and `&`
Now that you know the differences between `do...end` and `{}`, and how to use the `&` shorthand, you have several tools to write more concise and readable Ruby code. The choice between these syntaxes depends on the context and your personal or team’s coding style.

- **`do...end`**: Best for multi-line blocks where you want to perform several operations or enhance readability.
- **`{}`**: Ideal for single-line blocks or when you want to embed the block in a larger expression.
- **`&`**: Perfect for calling simple methods on each element of a collection in a concise way.

## Conclusion
Enumerables are a powerful set of tools in Ruby that allow us to work with collections more effectively. With methods like `map`, `select`, `reject`, `find`, and `find_all`, we can write more concise and readable code to manipulate and search collections.

---

- Approximately how long (in minutes) did this lesson take you to complete?
{: .free_text_number #time_taken title="Time taken" points="1" answer="any" }
