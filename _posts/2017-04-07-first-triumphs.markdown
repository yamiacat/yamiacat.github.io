---
layout: post
title:  "Early Triumphs"
date:   2017-04-07 15:33:33 +0000
categories: ruby week0 metal
---
I've been working my way through Chris Pine's excellent [book on ruby](https://pine.fm/LearnToProgram/) which sets you various challenges as you go. I got a greater sense of accomplishment from tackling these exercises than anything I did on Codecademy, in large part because I was creating files from scratch with a code editor, and then running them from the command line. The sort of virtual environment that Codecademy provides is great for giving instant feedback, but lacks a certain authenticity....

Anyway, an early task involves writing a little program that converts a number to its Roman numeral equivalent. Initially, old style Roman numerals, which are purely additive, so 4 is IIII, and 9 is VIIII. I found that task fairly straightforward, although if you [look at my code](https://github.com/yamiacat/ruby_practice/blob/master/nums_old_roman.rb) you can see that I haven't yet managed to grok modulo division. Like, at all.

The follow up task was to convert to 'new' Roman numerals, where 4 is IV and 9 is IX, and all that subtractive nonsense. This had me stumped for while. I worked on it without much success for the best part of a day. I found that I was still thinking about it over night, and when I woke in the morning I had some additional ideas about how to proceed, which was pretty gratifying!

I'll present it here in all its Rube Goldbergian glory! Some features of note:

- The number gets converted to a string, because at this point I know how to split strings, but not integers.
- The inclusion of a 'prep_array' full of zeros, because if I'm working with 4 digit numbers, how else would I handle less digits?!
- A comment about the .drop array method, which doesn't actually get used in the finished program. (And which I haven't yet found the answer for, but trial and error during testing suggests 'yes'.)

{% highlight ruby %}
def rome(n)
  prep_array = [0,0,0]
  first_array = n.to_s.split(//)
  rome_array = prep_array + first_array
     # DOES .drop(n) START COUNTING AT ZERO FROM THE OTHER END!?
 in_roman =""


in_roman += "M" * rome_array[-4].to_i

 hunds = rome_array[-3].to_i
  if hunds == 9
    in_roman += "CM"
  elsif hunds == 4
    in_roman += "CD"
  else
    in_roman += "D" * (hunds / 5) 
    in_roman += "C" * (hunds % 5) 
  end


 tens = rome_array[-2].to_i
  if tens == 9
    in_roman += "XC"
  elsif tens == 4
    in_roman += "XL"
  else
    in_roman += "L" * (tens / 5) 
    in_roman += "X" * (tens % 5) 
  end

 ones = rome_array[-1].to_i
  if ones == 9
    in_roman += "IX"
  elsif ones == 4
    in_roman += "IV"
  else
    in_roman += "V" * (ones / 5) 
    in_roman += "I" * (ones % 5) 
  end

  return in_roman

end

puts "Gimme a number between 1 and 3500 and I'll give you the new timey Roman numerals version!"

input = gets.chomp.to_i

if input <= 0 || input > 3500
  puts "Just gimme a number within the range, wiseguy!"
else
  puts rome(input)
end
{% endhighlight %}

So yeah - I'm sure there are MUCH more elegant ways of solving this task, and I clearly still don't grok modulo division, but I was very proud of myself for putting together something that worked, based on my 2 weeks or so of ruby study!

Also, this Entombed album cover suddenly makes a lot more sense:

![Entombed DCLXVI Album Cover]({{ site.url }}/assets/entombed-dclxvi.jpg)

666 = DCLXVI  
