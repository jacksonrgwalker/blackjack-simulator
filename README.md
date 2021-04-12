# blackjack-simulator

A simple, pure python simulator for the card game blackjack.

```python

from blackjack import Player, Dealer, Table, Game, DealerStrat


jack = Player(strategy = DealerStrat(max_hit_value=18), name='Jack')
zack = Player(strategy = DealerStrat(max_hit_value=17), name='Zack')
cody = Player(strategy = DealerStrat(max_hit_value=16), name='Cody')

dealer=Dealer(strategy = DealerStrat(max_hit_value=16))

big_table = Table(dealer, players=[jack,zack,cody])

game = Game(table=big_table)
game.simulate_rounds(1, verbose=True, delay=1)

game.summary()

```