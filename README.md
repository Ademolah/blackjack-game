# blackjack-game
import random

suits=('hearts','diamonds','spades','clubs')
ranks=('two','three','four','five','six','seven','eight','nine','ten','jack','queen','king','ace')
values={'two':2,'three':3,'four':4,'five':5,'six':6,'seven':7,'eight':8,'nine':9, 'king':10, 'queen':10,'jack':10,'ace':11}
playing = True

class Card:
    
    def __init__(self,suit,rank):
        self.suit=suit
        self.rank=rank
    
    def __str__(self):
        return self.rank + 'of' +self.suit
        
        class Deck:
    
    def __init__(self):
        self.deck=[]
        for suit in suits:
            for rank in ranks:
                self.deck.append(Card(suit,rank))
                
    def __str__(self):
        deck_comp = ''
        for card in self.deck:
            deck_comp += '\n ' +card.__str__()
        return 'The deck has:' + deck_comp
    
    def shuffle(self):
        random.shuffle(self.deck)
        
    def deal(self):
        single_card = self.deck.pop()
        return single_card
        
        class Hand:
    def __init__(self):
        self.cards=[]
        self.value=0
        self.aces=0
        
    def add_card(self, card):
        self.cards.append(card)
        self.value += values[card.rank]
        
    def adjust_for_ace(self):
        pass
        
        test_deck = Deck()
test_deck.shuffle()
test_player = Hand()
test_player.add_card(test_deck.deal())
test_player.add_card(test_deck.deal())
test_player.value

for card in test_player.cards:
    print(card)
    
    class Hand:
    def __init__(self):
        self.cards = []
        self.value =0
        self.aces = 0
        
    def add_card(self, card):
        self.cards.append(card)
        self.value += values[card.rank]
        if card.rank == 'ace':
            self.aces +=1
            
    def adjust_for_ace(self):
        while self.value > 21 and self.aces:
            self.value -= 10
            self.aces -= 1
            
            class Chips:
    def __init__(self):
        self.total = 100
        self.bet = 0
        
    def win_bet(self):
        self.total += self.bet
        
    def lose_bet(self):
        self.total -= self.bet
        
        def take_bet(chips):
    
    while True:
        try:
            chips.bet = int(input('how many chips would you like to bet? '))
        except:
            print('sorry, a bet must be an integer')
        else:
            if chips.bet>chips.total:
                print('sorry your bet cant exceed', chips.total )
            else:
                print('you just bet')
                break
                
    def hit(deck, hand):
    
        hand.add_card(deck.deal())
        hand.adjust_for_ace()
        
def hit_or_stand(deck, hand):
    global playing
    
    while True:
        x = input("would you like to Hit or stand? Enter 'h' or 's'  ")
        
        if x[0].lower()== 'h':
            hit(deck, hand)
            
        elif x[0].lower() == 's':
            print("player stands. Dealer is playing")
            playing = False
            
        else:
            print('sorry, please try again')
            continue
        break
               
def show_some(player, dealer):
    print("\nDealer hand")
    print(" <card hidden>")
    print('', dealer.cards[1])
    print("\nPlayer hand", *player.cards, sep ='\n ')
    
def show_all(player, dealer):
    print("\nDealer hand:", *dealer.cards, sep='\n ')
    print("Dealer hand =", dealer.value)
    
    def player_busts(player,dealer,chips):
    print("player busts!")
    chips.lose_bet()
    
def player_wins(player, dealer, chips):
    print("player wins")
    chips.win_bet()
    
def dealer_busts(player, dealer, chips):
    print("dealer bursts!")
    chips.win_bet()
    
def dealer_wins(player, dealer, chips):
    print("dealer wins!")
    chips.lose_bet()
    
def push(player, dealer):
    print("dealer and player tie! its a push.")
    print("\nPlayer hand:", *player.cards, sep='\n ')
    print("Player hand =", player.value)
    
while True:
    # Print an opening statement
    print('Welcome to BlackJack! Get as close to 21 as you can without going over!\n\
    Dealer hits until she reaches 17. Aces count as 1 or 11.')
    
    # Create & shuffle the deck, deal two cards to each player
    deck = Deck()
    deck.shuffle()
    
    player_hand = Hand()
    player_hand.add_card(deck.deal())
    player_hand.add_card(deck.deal())
    
    dealer_hand = Hand()
    dealer_hand.add_card(deck.deal())
    dealer_hand.add_card(deck.deal())
            
    # Set up the Player's chips
    player_chips = Chips()  # remember the default value is 100    
    
    # Prompt the Player for their bet
    take_bet(player_chips)
    
    # Show cards (but keep one dealer card hidden)
    show_some(player_hand,dealer_hand)
    
    while playing:  # recall this variable from our hit_or_stand function
        
        # Prompt for Player to Hit or Stand
        hit_or_stand(deck,player_hand) 
        
             
        # Show cards (but keep one dealer card hidden)
        show_some(player_hand,dealer_hand)  
        
        # If player's hand exceeds 21, run player_busts() and break out of loop
        if player_hand.value > 21:
            player_busts(player_hand,dealer_hand,player_chips)
            break        


    # If Player hasn't busted, play Dealer's hand until Dealer reaches 17 
    if player_hand.value <= 21:
        
        while dealer_hand.value < 17:
            hit(deck,dealer_hand)    
    
        # Show all cards
        show_all(player_hand,dealer_hand)
        
        # Run different winning scenarios
        if dealer_hand.value > 21:
            dealer_busts(player_hand,dealer_hand,player_chips)

        elif dealer_hand.value > player_hand.value:
            dealer_wins(player_hand,dealer_hand,player_chips)

        elif dealer_hand.value < player_hand.value:
            player_wins(player_hand,dealer_hand,player_chips)
            
        else:
            push(player_hand,dealer_hand)        
    
    # Inform Player of their chips total 
    print("\nPlayer's winnings stand at",player_chips.total)
    
    # Ask to play again
    new_game = input("Would you like to play another hand? Enter 'y' or 'n' ")
    
    if new_game[0].lower()=='y':
        playing=True
        continue
    else:
        print("Thanks for playing!")
        break
        
        
    
    
    
