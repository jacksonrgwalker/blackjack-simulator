
# blackjack-simulator

A simple, pure python simulator for the card game blackjack.

You can simulate a game by first initializing the players along with the dealer.
```python
from blackjack import Player, Dealer, Table, Game, DealerStrat

jack = Player(strategy = DealerStrat(max_hit_value=18), name='Jack')
zack = Player(strategy = DealerStrat(max_hit_value=17), name='Zack')
cody = Player(strategy = DealerStrat(max_hit_value=16), name='Cody')

dealer=Dealer(strategy = DealerStrat(max_hit_value=16))
```

The `DealerStrat` is a simple strategy that most casino dealers are directed to follow: you must hit if you are below a certain threshold, otherwise stay.

Now, we the players sit around a table and start the game.

```python
big_table = Table(dealer, players=[jack,zack,cody])

game = Game(table=big_table)
game.simulate_rounds(1, verbose=True, delay=1)
```
![example clip](example.gif)

You can access a summary of the game.
```python
game.summary()
```
```python
Number of rounds simulated:          3
Jack | Win Rate: 0.6667 | Draw Rate: 0.0000
Zack | Win Rate: 0.3333 | Draw Rate: 0.0000
Cody | Win Rate: 0.6667 | Draw Rate: 0.0000
```

You can compare strategies by simulating many rounds.

```python
players = [Player(strategy = DealerStrat(max_hit_value=i), name=f'Max Hit on {i}') for i in range(9,21)]
dealer=Dealer(strategy = DealerStrat(max_hit_value=16))
big_table = Table(dealer, players=players)
game = Game(table=big_table, min_cards_to_reshuffle=50)
game.simulate_rounds(50_000, verbose=False, delay=0)
game.summary()
```
```python
Number of rounds simulated:     50,000
Max Hit on 9 | Win Rate: 0.3866 | Draw Rate: 0.0595
Max Hit on 10 | Win Rate: 0.3980 | Draw Rate: 0.0632
Max Hit on 11 | Win Rate: 0.4108 | Draw Rate: 0.0694
Max Hit on 12 | Win Rate: 0.4150 | Draw Rate: 0.0728
Max Hit on 13 | Win Rate: 0.4174 | Draw Rate: 0.0820
Max Hit on 14 | Win Rate: 0.4172 | Draw Rate: 0.0875
Max Hit on 15 | Win Rate: 0.4101 | Draw Rate: 0.0985
Max Hit on 16 | Win Rate: 0.4064 | Draw Rate: 0.1041
Max Hit on 17 | Win Rate: 0.3993 | Draw Rate: 0.0896
Max Hit on 18 | Win Rate: 0.3611 | Draw Rate: 0.0759
Max Hit on 19 | Win Rate: 0.2931 | Draw Rate: 0.0596
Max Hit on 20 | Win Rate: 0.1541 | Draw Rate: 0.0226
```
![bar chart](results.gif)
