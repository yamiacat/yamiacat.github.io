---
layout: post
title:  "Classes, Pair Programming, and Snakes & Ladders"
date:   2017-04-20 16:00:33 +0000
categories: blogpost week2 ruby
comments: true
---
*If you're just here to moc-, uh, provide feedback on my code, scroll down!*

I haven't been blogging quite as often as I'd like because the course is kicking my ass, endurance-wise. Loving it though. We've been introduced to two big programming concepts so far this week. The first concept comes from the pure clean abstraction of the code-realm, where we've started to use **classes**. These will become our preferred way of doing pretty much everything once we've harnessed their power, I am told.

We briefly looked at class diagrams, which are a quick and dirty planning tool where you can sketch out a box for each class your software will have, and inside each box is a list of attributes it will have, what form they will take, and also a list of any functions they will have built into them.

For homework on Tuesday we were asked to think about how we'd write the mechanics for a game of [Snakes & Ladders](https://en.wikipedia.org/wiki/Snakes_and_Ladders), and draw class diagrams to suit. My first attempt didn't take too long, although in retrospect that's because I didn't think about it deeply enough:

![Class Diagram 1st Draft]({{site.url}}/assets/ClassDiagram.JPG "First draft of my class diagram for snakes and ladders")

I decided early on that 'snakes' and 'ladders' could be merged together because they basically did the same thing. You step on the square, and you appear elsewhere. They're basically teleporters, so I labelled them accordingly.

Going to bed happy with my efforts, I randomly awoke at 5AM and was unable to return to sleep. Thanks brain! Given some bonus time, I went back to my class diagram and realised that game squares that don't have teleporters on them don't really need to be defined. They're just numbers with no special properties so my class diagram shrank to two, and teleporters became "interesting game squares":

![Class Diagram 2nd Draft]({{site.url}}/assets/ClassDiagram2.JPG "Second draft of my class diagram for snakes and ladders")

Upon arrival at CodeClan Wednesday morning our cohort compared ideas, and immediately noted an extreme diversity of approach. Some people had six or seven classes, there were three or four different ideas about how to implement a game board, and a good deal of debate about which snakes & ladders 'house rules' should be included. 1d6 or 2d6? Do you need to throw a 6 to start? Are there any circumstances under which you'd get a free bonus go?

At this point we were introduced to our second big programming concept, this time from the messy chaotic meat-realm. **Pair programming**. Also known as 'programming out loud', this is the practice of two developers sharing a laptop and working on the same code. The person with fingers on keys is the 'driver', and the person watching is the 'navigator', in a partnership not dissimilar to rally driving, except you stop every 20 minutes or so and swap roles, and a momentary lapse in concentration poses little risk to roadside spectators.

Some of the cohort found it a bit stressful, but I freaking loved it. Having another set of eyes (and the mind behind them) following your code means you're much less likely to leave a bracket unclosed or add an extraneous `=` which destroys everything and takes tens of minutes to track down. It also gives you a sounding board for ideas, and a check on wandering too far off the path that you had planned out.

I was paired with the delightful [Charlie Wood](@ch4rlie_wood). And as we compared diagrams, the gaping holes in mine quickly became apparent. I'd planned out the game board and the players, but had given no thought to how to regulate who's turn it was, or determine how a player could win! Doh! After a rapidly revised third draft, I ended up with a class diagram that looks like this:

![Class Diagram 4th Draft]({{site.url}}/assets/ClassDiagram4.JPG "Fourth draft of my class diagram for snakes and ladders")

We had five hours to pair program this into existence. We were told not to worry about user interaction - just code the rules of the game. It was an absorbing, though draining five hours, and in the end we managed to cobble something together that more or less works!

The code we came up with is below. It, uh... It felt like we wrote a LOT more than that. (Well, with all the testing, we did - the full project is on GitHub [here.](https://github.com/yamiacat/snakes-n-ladders-matt-n-charlie)) But seriously - dropped into two boxes on a website that does not look like a lot of code!

Game Class:

{% highlight ruby %}
class Game

  attr_reader :players, :players_index_position, :board

  def initialize
    @players = []
    @players_index_position = []

    @board = {
      5 => 2,
      13 => 10,
      39 => 19,
      45 => 5,
      60 => 11,
      67 => 9,
      80 => 15,
      91 => 3,
      12 => -3,
      19 => -15,
      28 => -13,
      51 => -32,
      72 => -21,
      79 => -9,
      82 => -12,
      99 => -50
    }

  end

  def add_player(player_to_be_added)
    @players << player_to_be_added
  end

  def start_game
    number_of_players = @players.count
    until number_of_players == 0
      number_of_players -= 1
      @players_index_position << number_of_players
    end
  end

  def next_player
    @players_index_position.rotate!
    up_next = @players_index_position.first
    return @players[up_next]
  end
end
{% endhighlight %}


Player Class:

{% highlight ruby %}
class Player

  attr_reader :name
  attr_accessor :location

  def initialize(name)
    @name = name
    @location = 0

  end

  # def win
  #   finish_line = 11
  #   return "#{@name} wins!" if @location >= finish_line
  #
  # end

  def move(board)
    finish_line = 100

    d6 = [1,2,3,4,5,6]
    # d6.shuffle.first  <-- replace 5 below with this
    @location += d6.shuffle.first
    if board.has_key?(@location) == true
      @location += board[@location]
    end

    return "#{@name} wins!" if @location >= finish_line

  end
end

{% endhighlight %}

A few notes:

* As we wrote the program, it shrank back down to two classes. The information in the 'Interesting Game Squares' moved into the Game class, and lived in a hash. The automove function just became part of the player's move function.

* I'm quite pleased with the elegance of my dice mechanic. Put the numbers one to six in an array and call `.shuffle.first` on it! ^-^

* For most of the development process we kept the dice mechanic commented out, because we were advised that trying to test our software while there was a random element in play was not going to end well! We just said that every move was 5 during testing.

* I'm less pleased with the elegance of the turn taking system, which actually took up most of the coding time. Upon trying to implement it, we realised we were also going to need to create a function to 'add players' to the game, and a 'start game' function that would count the number of players and cycle through them as they take turns. I suggested a second array that kept index positions for the players within the player array, but that feels... cludgy.

* Charlie had the brainwave of combining the win condition check into the move function. You can still see our early attempts at a separate win function check that has been commented out!

* We ran out of time before being able to add a function that demands you get an exact throw to finish the game. I suspect we would have bunged that into the move function too!

Any comments or advice gratefully received, either here or directed at @mrjesslynnrose !



{% if page.comments %} <div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://futuremorlock.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript> {% endif %}
