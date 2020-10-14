---
layout: post
title: "Does Point Balance Correlate with Success in the NBA?"
mathjax: true
---

Point Balance (PB) is a metric introduced by Stephen Shea and Christopher Baker in their 2013 book, [Basketball Analytics]. It measures how balanced a team is in scoring, a high score means the team has a high distribution of scoring vs a low score which tells us only a few players do most of the scoring.

It is calculated by the distribution of points divided by the distribution of minutes which are defined by :

$$ D(pts) = - \sum p_i * log_2(p_i)$$

$$ D(min) = - \sum m_i * log_2(m_i)$$

where \\(p_i \\) and \\(m_i \\) are the total points and minutes for player i respectively, thus leading to

$$ PB = \frac{D(pts)}{D(min)} $$



The goal of this article is to determine if the Point Balance of a team has any correlation with its success, or even just its offensive success. For every team from 2011-2020, I calculated its PB score and took the winning percentage, offensive rating, [effective FG%], whether or not that team made the playoffs, and whether or not that team won the finals.

The overall average PB score for NBA teams over the last 10 years has been 0.955. The lowest PB score we saw was 0.862, by the 2011 ‘Big 3’ Miami Heat who ended up losing in the finals. The highest was 1.008 by the 2017 Philadelphia 76ers, who had a number of players suffer injuries throughout the season and went 28-54. The average score for playoff teams is 0.948 versus 0.963 for teams that missed the cut. Going further, those playoff teams that won the championship had an average of 0.939. So off the bat, it does seem to correlate at least a little bit. Below are the boxplots which help visualize the averages a little bit more, as well as the win percentage of teams plotted against their PB score.

<!-- ![](/assets/playoff_box.png)![](/assets/champ_box.png) -->

<p align="center">
  <img width="365" src="/assets/playoff_box.png">
  <img width="365" src="/assets/champ_box.png">
</p>

![](/assets/wpct_pb.png){: .align-right}

This trend even coincides a little bit with how efficient the team’s offense is. In the 2 categories I looked at, offensive rating and effective field goal percentage, there proved to be a negative correlation.

<p align="center">
  <img width="365" src="/assets/ortg_pb.png">
  <img width="365" src="/assets/efg_pb.png">
</p>

Now obviously these aren’t the strongest correlations, shown by their R^2 values, but there is definitely a general trend. Teams led by the few generally do better than teams led by the many.

Look at the highest and lowest PB scores by year. Only 1 team made the playoffs having the highest PB score, the 2013 Denver Nuggets who had 5 guys scoring double digits and Ty Lawson leading the team at 16.7 ppg. They lost in the first round in 6 games. The minimum PB scores had an overall win percentage of 0.431. On the other end, not a single team missed the playoffs when they had the highest PB score, granted 6 of those years were the Thunder and 2 had Lebron. These scores had an overall win percentage of 0.641, yet interestingly, not a single one was able to seize the Larry O’Brien Trophy.

### Highest
<table>
  {% for row in site.data.year_max %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}

    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
</table>

### Lowest
<table>
  {% for row in site.data.year_min %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}

    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
</table>

So what does this mean? Would the 10-72 76ers have been better if they gave rookie Jahlil Okafor 10 more touches a game to increase his scoring? Of course not. But it shows that something that we all probably knew, stars run the NBA. Teams need guys that can and will take over a game to get wins. With this though, it’s not really a surprise that the lowest score never won the championship. Stars only get you so far. For example, the 2011 Heat who just got the Big 3 had the lowest score in the last 10 years. In the finals, when LeBron doesn’t play like his usual self it is hard to overcome that hole if there aren’t other players who can step up. Fast forward a year, a few guys like Mario Chalmers improved and the team brought in some new players like Shane Battier. Funnily enough, when they reached the finals, it was against a team in a similar position as the previous Heat team. 3 budding stars and not much other help. Looking at other championship teams, it's no surprise what the high PB teams were. The 2014 Spurs, 2019 Raptors, and 2011 Mavericks are the top 3 respectively and were all considered great and deep ‘teams’ vs the star lead Heat and Warriors. So the formula to raise a trophy in the NBA is simple, get some stars, but also get some solid role players around those stars. That can’t be too hard right?

### Champions
<table>
  {% for row in site.data.cham_pb %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}

    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
</table>

Just for fun, here are the highest and lowest PB scores for each team over the last 10 years.

### Highest
<table>
  {% for row in site.data.team_max %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}

    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
</table>

### Lowest
<table>
  {% for row in site.data.team_min %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}

    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
</table>


The full code for scraping the data, analyzing it, plus the output images and tables can be found on my Github account [here]. All stats were scraped from [basketball-reference.com].


[Basketball Analytics]: https://books.google.com/books/about/Basketball_Analytics.html?id=f1IbnwEACAAJ
[effective FG%]: https://www.basketball-reference.com/about/glossary.html
[here]: https://github.com/ckirch8/NBA_Point_Balance
[basketball-reference.com]: https://www.basketball-reference.com
