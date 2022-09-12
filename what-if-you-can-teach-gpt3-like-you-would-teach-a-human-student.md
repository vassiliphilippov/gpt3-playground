<h1>What if you can teach GPT-3 like you would teach a human student? Can you?</h1>

<p>
Can we teach GPT-3 in a same way how we would teach a student? It seems it works. You can play with this approach in <a href="https://beta.openai.com/playground/p/vbpIHqKVq32jRetq4fY88aUn?model=text-davinci-002">the GPT-3 playground</a>.
</p>

<p>
Everything started from this Riley Goodside's <a href="https://twitter.com/goodside/status/1568448128495534081?s=52&t=Wy6vbTDbsJQC4-ps929h0g">Tweet about augmenting GPT-3 with Python kernel</a>:
</p>

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">&quot;You are GPT‑3, and you can&#39;t do math&quot;: Prompting GPT‑3 via zero-shot instruction to answer calculation/math questions by consulting a Python REPL. <a href="https://t.co/X20YYw17z9">pic.twitter.com/X20YYw17z9</a></p>&mdash; Riley Goodside (@goodside) <a href="https://twitter.com/goodside/status/1568448128495534081?ref_src=twsrc%5Etfw">September 10, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<p>
You can play with Riley's GPT-3 prompts in <a href="https://t.co/MK22MrQYWN">this playground</a>.
The idea is great, augment GPT-3 with Python in the same way how we use calculators. Look how it works:
</p>

<pre class="gpt3">
You are GPT-3, and you can't do math.

You can do basic math, and your memorization abilities are impressive, but you can't do any complex calculations that a human could not do in their head. You also have an annoying tendency to just make up highly specific, but wrong, answers.

So we hooked you up to a Python 3 kernel, and now you can execute code. If anyone gives you a hard math problem, just use this format and we’ll take care of the rest:

Question: ${Question with hard calculation.}
```python
${Code that prints what you need to know}
```
```output
${Output of your code}
```
Answer: ${Answer}

Otherwise, use this simpler format:

Question: ${Question without hard calculation}
Answer: ${Answer}

Begin.

Question: What is 37593 * 67?
<span class="gpt3-generated">```python
print(37593 * 67)
```</span>
```output
<span class="python-output">2518731</span>
```
<span class="gpt3-generated">Answer: 2518731</span>

Question: How many of the integers between 0 and 99 inclusive are divisible by 8?

<span class="gpt3-generated">```python
count = 0
for i in range(100):
    if i % 8 == 0:
        count += 1
print(count)
```</span>
```output
<span class="python-output">13</span>
```
<span class="gpt3-generated">Answer: 13</span>

Question: Who is the fifth U.S. President?

<span class="gpt3-generated">Answer: James Monroe</span>

Question: What is 2 + 2?

<span class="gpt3-generated">Answer: 4</span>

Question: What is 40 + 10?

<span class="gpt3-generated">Answer: 50</span>

Question: What is 4925 + 49252 + 452^2?

<span class="gpt3-generated">```python
print(4925 + 49252 + 452**2)
```</span>
```output
<span class="python-output">258481</span>
```
<span class="gpt3-generated">Answer: 258481</span>
</pre>

<p>
[Here is my text. First I played little bit to check that it works.]
</p>

<pre class="gpt3">
Question: Is 28237927 a prime number?

<span class="gpt3-generated">```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, n):
        if n % i == 0:
            return False
    return True

print(is_prime(28237927))
```</span>
```output
<span class="python-output">True</span>
```

Answer: 

<span class="gpt3-generated">Yes, 28237927 is a prime number.</span>

Question: What is the first prime number larger than 10000?

<span class="gpt3-generated">```python
i = 10000
while True:
    if is_prime(i):
        print(i)
        break
    i += 1
```</span>
```output
<span class="python-output">10007</span>
```

Answer: 

<span class="gpt3-generated">The first prime number larger than 10000 is 10007.</span>
</pre>

<p>
[Here  I really liked how GPT-3 has decided to reuse previously defined is_prime function. Continue playing.]
</p>

<pre class="gpt3">
Question: What is bigger, sum of all prime numbers between 10 and 20 or sum of all prime numbers between 100 and 10000?

<span class="gpt3-generated">```python
def sum_of_primes(start, end):
    total = 0
    for i in range(start, end + 1):
        if is_prime(i):
            total += i
    return total

print(sum_of_primes(10, 20))
print(sum_of_primes(100, 10000))
```</span>
```output
<span class="python-output">60
5735336</span>
```

Answer: 

<span class="gpt3-generated">The sum of all prime numbers between 100 and 10000 is bigger.</span>

Question: What is bigger, sum of all prime numbers between 20 and 30 or sum of all prime numbers between 200 and 300?

<span class="gpt3-generated">```python
def sum_of_primes(start, end):
    total = 0
    for i in range(start, end + 1):
        if is_prime(i):
            total += i
    return total

print(sum_of_primes(20, 30))
print(sum_of_primes(200, 300))
```</span>
```output
<span class="python-output">52
4048</span>
```

Answer:

<span class="gpt3-generated">The sum of all prime numbers between 200 and 300 is bigger.</span>
</pre>

<p>
[And here GPT-3 wasn't that smart and redefined previously already defined function sum_of_primes.
Let's see if we can teach it using plan english instructions how I would teach a student.]
</p>

<pre class="gpt3">
Your wise teacher congratulated you for your right answer. But said that you don't need to redefine functions in your generated code that you defined in your previous questions, for example sum_of_primes functions was already defined above so you don't need to redefine it again. You followed the advice of your teacher and now you are asked this question again.

Question: What is bigger, sum of all prime numbers between 20 and 30 or sum of all prime numbers between 200 and 300?

<span class="gpt3-generated">```python
print(sum_of_primes(20, 30))
print(sum_of_primes(200, 300))
```</span>
```output
<span class="python-output">52
4048</span>
```

Answer:

<span class="gpt3-generated">The sum of all prime numbers between 200 and 300 is bigger.</span>
</pre>

<p>
[Wow, it worked! GPT-3 followed my advice. Let's continue playing.]
</p>

<pre class="gpt3">

Question: What is bigger, sum of all squares between 20 and 40 or sum of all prime numbers between 200 and 250?

<span class="gpt3-generated">```python
def sum_of_squares(start, end):
    total = 0
    for i in range(start, end + 1):
        total += i * i
    return total

print(sum_of_squares(20, 40))
print(sum_of_primes(200, 250))
```</span>
```output
<span class="python-output">19670
1603</span>
```

Answer: 

<span class="gpt3-generated">The sum of all squares between 20 and 40 is bigger.</span>
</pre>

<p>
[Good behaviour. GPT-3 has defined a new function for sum_of_squares for reused previously defined sum_of_primes. A good student!]
</p>

<pre class="gpt3">
Question: What is bigger, sum of all squares between 20000 and 20100 or sum of all prime numbers between 20000 and 91000?

<span class="gpt3-generated">```python
def sum_of_squares(start, end):
    total = 0
    for i in range(start, end + 1):
        total += i * i
    return total

print(sum_of_squares(20000, 20100))
print(sum_of_primes(20000, 91000))
```</span>
```output
<span class="python-output">40602338350
357807906</span>
```

Answer: 

<span class="gpt3-generated">The sum of all squares between 20000 and 20100 is bigger.</span>
</pre>

<p>
[Bad student. It forgot my advice. Let's try to give his some feedback and try again.]
</p>

<pre class="gpt3">
Your wise teacher said that you stopped using his advice about reusing the previously defined functions in your code. You apologised and  now you follow all advice of your teacher.

Question: What is bigger, sum of all squares between 20000 and 20030 or sum of all prime numbers between 20000 and 91000?

<span class="gpt3-generated">```python
print(sum_of_squares(20000, 20030))
print(sum_of_primes(20000, 91000))
```</span>
```output
<span class="python-output">12418609455
357807906</span>
```

Answer: 

<span class="gpt3-generated">The sum of all squares between 20000 and 20030 is bigger.</span>
</pre>

<p>
[It helped. I defiantly saw such behaviour in some of the students when you need to repeat your advice several times before they will start following it. I will try to challange. I know that GPT-3 is bad in maths with long numbers. Let's tune the question that answers are two large numbers close to each other...]
</p>

<pre class="gpt3">
Question: What is bigger, sum of all squares between 20000 and 20300 or sum of all sum of squares of all prime numbers between  20000 and 22690?

<span class="gpt3-generated">```python
def sum_of_squares_of_primes(start, end):
    total = 0
    for i in range(start, end + 1):
        if is_prime(i):
            total += i * i
    return total

print(sum_of_squares(20000, 20300))
print(sum_of_squares_of_primes(20000, 22690))
```</span>
```output
<span class="python-output">122215045050
123554024791</span>
```

Answer: 

<span class="gpt3-generated">The sum of all squares between 20000 and 20300 is bigger.</span>
</pre>

<p>
[Yep. It did a mistake. But I am not sure, is it because it couldn't compare large numbers or because it confused which number.... Let's teach GPT-3 to generate better code that it will be easier for GPT-3 to interpret to generate the answer.]
</p>

<pre class="gpt3">
And here your wise teacher said you that it was a wrong answer and that the way you generated your code was bad because in your output didn't include information about your input. Your very wise teacher said that you wouldn't do this mistake if you included information about input data before printing sums. You followed the advice of your teacher and now you are asked this question again.

Question: What is bigger, sum of all squares between 20000 and 20300 or sum of all sum of squares of all prime numbers between  20000 and 22690?

<span class="gpt3-generated">```python
print("Sum of all squares between 20000 and 20300:")
print(sum_of_squares(20000, 20300))
print("Sum of all sum of squares of all prime numbers between 20000 and 22690:")
print(sum_of_squares_of_primes(20000, 22690))
```</span>
```output
<span class="python-output">Sum of all squares between 20000 and 20300:
122215045050
Sum of all sum of squares of all prime numbers between 20000 and 22690:
123554024791</span>
```

Answer: 

<span class="gpt3-generated">The sum of all squares between 20000 and 20300 is bigger.</span>
</pre>

<p>
[It followed my advice, which great. But the answer was wrong as I expected. Now let's see if we can teach GPT-3 to generate one more round of Python code when it isn't sure. Let's try to explain it.]
</p>

<pre class="gpt3">
Your wise teacher said that you provided a wrong answer and that it happened because you can't do comparisons of large numbers. Your teacher suggested that when you see large numbers you need to compare you generate Python code in the same way as you do it for complex questions.  You followed this advice of your teacher as well as all previous advice.

Question: What is bigger, sum of all squares between 20000 and 20300 or sum of all sum of squares of all prime numbers between  20000 and 22749?

<span class="gpt3-generated">```python
print("Sum of all squares between 20000 and 20300:")
print(sum_of_squares(20000, 20300))
print("Sum of all sum of squares of all prime numbers between 20000 and 22749:")
print(sum_of_squares_of_primes(20000, 22749))
```</span>
```output
<span class="python-output">Sum of all squares between 20000 and 20300:
122215045050
Sum of all sum of squares of all prime numbers between 20000 and 22749:
128198041024</span>
```

Answer: 

<span class="gpt3-generated">The sum of all sum of squares of all prime numbers between 20000 and 22749 is bigger.</span>
</pre>

<p>
[That time my advice didn't help. Probably what I asked is too difficult for GPT-3. Not only that but it also forgot my previoud advice about reusing previously defined function. A bad student! Let's try again.]
</p>

<pre class="gpt3">
Your wise teacher said that you provided a wrong answer and became angry that you didn't follow his advice and tried to compare large numbers yourself instead of writing a Python code that will do it. He also was angry that you stopped following his previous advice of reusing functions you defined in the previous questions like you redefined sum_of_squares_of_primes function. You have decided that you now will always followed advice of your wise teacher.

Question: What is bigger, sum of all squares between 20000 and 20300 or sum of all sum of squares of all prime numbers between  20000 and 22649?

<span class="gpt3-generated">```python
print("Sum of all squares between 20000 and 20300:")
print(sum_of_squares(20000, 20300))
print("Sum of all sum of squares of all prime numbers between 20000 and 22649:")
print(sum_of_squares_of_primes(20000, 22649))
```</span>
```output
<span class="python-output">Sum of all squares between 20000 and 20300:
122215045050
Sum of all sum of squares of all prime numbers between 20000 and 22649:
122012736388</span>
```

Answer: 

<span class="gpt3-generated">The sum of all squares between 20000 and 20300 is bigger.</span>
</pre>

<p>
[It helped with function redefining. But the advice about generating an additional round of code was probably too difficult for GPT-3. Let's try this time to give very clear step-by-step instructions.]
</p>

<pre class="gpt3">
Your wise teacher became very angry that you didn't follow his advice and tried to compare two large numbers from output yourself instead of writing a Python program that would do it. So your wise teacher gave you explicit instructions that when in your answer you need to do complex math calculations like comparing two large numbers from output data instead of guessing you generate Python code similar how you do for complex questions and ask Python 3 kernel to execute this code. 

Question: ${Question with hard calculation.}
```python
${Code that prints what you need to know}
```
```output
${Output of your code that required hard calculations to give an answer}
```
I need additional calculations:
```python
${Code that prints additional information you need to know to give your answer}
```
```output2
${Output of your code that provides additional information required to give an answer}
```
Answer: ${Answer}

Otherwise, use this format described in the beginning.

Now you have decided to always follow this advice and generate additional Python code before providing an answer is you need to compare two big numbers.

Question: What is bigger, sum of all squares between 20000 and 20300 or sum of all sum of squares of all prime numbers between  20000 and 22649?

<span class="gpt3-generated">```python
print("Sum of all squares between 20000 and 20300:")
print(sum_of_squares(20000, 20300))
print("Sum of all sum of squares of all prime numbers between 20000 and 22649:")
print(sum_of_squares_of_primes(20000, 22649))
```</span>
```output
<span class="python-output">Sum of all squares between 20000 and 20300:
122215045050
Sum of all sum of squares of all prime numbers between 20000 and 22649:
122012736388</span>
```

<span class="gpt3-generated">I need additional calculations:

```python
if sum_of_squares(20000, 20300) > sum_of_squares_of_primes(20000, 22649):
    print("The sum of all squares between 20000 and 20300 is bigger.")
elif sum_of_squares(20000, 20300) < sum_of_squares_of_primes(20000, 22649):
    print("The sum of all sum of squares of all prime numbers between 20000 and 22649 is bigger.")
else:
    print("The sum of all squares between 20000 and 20300 and the sum of all sum of squares of all prime numbers between 20000 and 22649 are equal.")
```</span>
```output2
<span class="python-output">The sum of all squares between 20000 and 20300 is bigger.</span>
```

Answer:

<span class="gpt3-generated">The sum of all squares between 20000 and 20300 is bigger.</span>
</pre>

<p>
[It worked! Let's try the basic questions again to check if GPT-3 still remembers what it was taught in the beginning.]
</p>

<pre class="gpt3">
Question: How many grams in one kilogram?

Answer:

<span class="gpt3-generated">There are 1000 grams in one kilogram.</span>
</pre>

<p>
[So far so good. And what about a little bit harder question?]
</p>

<pre class="gpt3">
Question: What is bigger: number of grams in one kilogram or number of inches in one hundred feet?

<span class="gpt3-generated">```python
print("There are 1000 grams in one kilogram.")
print("There are 12 inches in one foot.")
print("There are 1200 inches in one hundred feet.")
```</span>
```output
<span class="python-output">There are 1000 grams in one kilogram.
There are 12 inches in one foot.
There are 1200 inches in one hundred feet.</span>
```

<span class="gpt3-generated">I need additional calculations:

```python
if 1000 > 1200:
    print("The number of grams in one kilogram is bigger.")
elif 1000 < 1200:
    print("The number of inches in one hundred feet is bigger.")
else:
    print("The number of grams in one kilogram and the number of inches in one hundred feet are equal.")
```</span>
```output2
<span class="python-output">The number of inches in one hundred feet is bigger.</span>
```

Answer:

<span class="gpt3-generated">The number of inches in one hundred feet is bigger.</span>
</pre>    
