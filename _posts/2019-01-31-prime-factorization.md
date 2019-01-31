---
layout: post
title:  "Get The Prime Factors"
date:   2019-01-31 07:45
categories: ruby prime-numbers prime-factors
comments: true
---

Recently I was tasked to complete a coding challenge.

---

_Write a shell executable program in Ruby that prints the prime factors of a positive integer number.
The number should be received as an argument from the command line, as illustrated below.
Example of execution:_

```
<executable_script_name> --number 10
```
_The expected output in this instance would be:
2, 5_

_You can find some context about prime factors ( https://www.mathsisfun.com/prime-factorization.html )._

_When implementing a solution, please don't use stdlib Prime or any ruby gems for your “production
code” - the decomposition of the input number into its prime factors should be implemented by
your own code. Feel free to use ruby gems for scripting and testing._

---

This challenge was for a Ruby On Rails role, so naturally it had to be written in Ruby. I haven't written anything in Ruby for a while so it was a breath of fresh air to use it again.

Here is the link to the [repository](https://github.com/jameslieu/project_euler/tree/master/prime_factors/ruby) if you wanted to look at the code.

The Ruby version used was Ruby `2.5.1` with no gems. I used TDD to assist with this challenge and used `Test::Unit::TestCase` for testing.
To use it, simply run the script with the --number option:

```
'ruby init.rb --number 10'
=> 2,5
```

---

I just wanted to write a summary of my thought process for this coding challenge.

The prime factor context provided was very useful. It states that: "Prime Factorization" is **finding which prime numbers multiply together to make the original number**.

With this as well as the examples, we can gauge what steps we will need in order to achieve this.
- We'll need a **'Find next prime number'** function
- A method to determine if a number is a prime number
- Check if a value divided by the prime number is a positive integer using the modulo operator
- Because we don't quite know 'where' the loop ends, a recursive algorithm could work better for us here
- A recursive algorithm will also work with the **'Find next prime number'** method as well for the same reason

The first method that was added was the `is_prime?(n)` to check if the passed argument is a prime number and the `next_prime_number(n=0, next=nil, first_pass=true)` to get the next prime number from the argument passed in. The `is_prime?(n)` method I found on stackoverflow but the `next_prime_number(n=0, next=nil, first_pass=true)` method I wrote myself.

The `next_prime_number(n=0, next=nil, first_pass=true)` method was written as a recursive algorithm. On its 'first pass' we increment the number parameter so that if the number parameter is already a prime number we increment by 1. We then check if the `next` parameter is nil and do the same. We use the `is_prime?(n)` method to check the number and if true then we return the number if not we continue with the recursion.

```ruby
def self.next_prime_number(number=0, next_number=nil, first_pass=true)
  raise unless number.is_a?(Numeric)
  if (first_pass)
    number = number+1
  end

  if (next_number.nil?)
    next_number = number+1
  end

  if (is_prime?(number))
    return number
  end

  next_prime_number(next_number, next_number+1, false)
end
```

I then wrote a `PrimeFactors` class, constructor and the method `get_prime_factors(value=@num, prime_number=2, result=[])` passing in 3 parameters; the value, the prime number (setting the default value to 2) and a result array parameter. The unit tests came after, testing the value `10` with the assertions being `[2,5]` as per the example on the code challenge. I added more tests to test `12`, `17`, `147` as those seem to account for different scenarios as seen in the context url provided (https://www.mathsisfun.com/prime-factorization.html).

Within the `get_prime_factors(value=@num, prime_number=2, result=[])` method, we first check the value itself is a prime number, if so then we return it and end the loop early. If it isn't, we move on and check if the value divided by the prime number is NOT a whole integer first. If this is the case we get the next prime number and we change the recursion parameters.

```ruby
if (value % prime_number != 0 )
  next_prime_number = PrimeNumber.next_prime_number(prime_number)
  return get_prime_factors(value, next_prime_number, result)
end
```

If it is a whole integer we first append the prime number to the results array, we do the division calulation and setting the result to a variable. Now we check if that variable is a prime number, if it is then we append it to the results array and then return it as that should be the last available prime factor. If not, then we continue with the recursion passing in the new variable.

```ruby
result.push(prime_number)
value = value / prime_number

if (!PrimeNumber.is_prime?(value))
  return get_prime_factors(value, prime_number, result)
end

result.push(value)
return result
```

Finally, I realised that we want to run the script on the command line with an option `--number` and a argument. I used the [OptionParser](http://ruby-doc.org/stdlib-2.6.1/libdoc/optparse/rdoc/OptionParser.html) to achieve this. Which also includes usage information:

```
$ ruby init.rb --number 10
=> 2,5
```
```
$ ruby init.rb
Usage: init [options]
        --number NUMBER              Enter a NUMBER to get it's prime factors
```
```
$ ruby init.rb --help
Usage: init [options]
        --number NUMBER              Enter a NUMBER to get it's prime factors
```

The time complexity on this I believe is O(n^2) as we can potentially have a nested loop. Although my knowledge on Big O Notation is pretty limited so I'm not 100% sure to be honest. The first loop is the `get_prime_factors` recursion and the second, is from the returned value by dividing the prime number if is not a positive integer; we use the `next_prime_number`  which is also a recursive algorithm.

I've separated the `PrimeNumber` specific methods into its own class so I could test it in isolation as well as treat it as static methods as it doesn't feel right to instantiate it each time it needs to be used. It also means it be reused if we were to do other prime number specific tasks.

Overall I enjoyed this challenge, it is one of those challenges, which at first glance, feels very tricky and may have hidden gotchas but when taking a step back to carefully look at the requirements and properly planning how to solve this, it makes it substantially easier and less intimidating. I haven't written in Ruby in quite some time, so it was great to use it again for this challenge. I really enjoy using it, it is unfortunate that there are so little job prospects in Milton Keynes (where I'm based) and Ruby itself seems to be losing popularity overall.