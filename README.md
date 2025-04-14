# Texas Hold'em Poker

A non-observable and zero-sum Poker (Texas Hold'em) game simulator with Expectiminimax algorithm for strategic decision-making in uncertain events. This repository contains a text-based Texas Hold'em Poker game implementation, where a user can play against AI players. The AI uses a basic Expectiminimax decision-making algorithm to decide its actions (such as fold, call, raise, or bluff). The game includes features like community cards, betting rounds, and showdown logic.

## Table of contents

- [Game Features](#game-features)
- [How to Run the Game](#how-to-run-the-game)
- [Methodology](#methodology)
- [Game Flow](#game-flow)
- [Gamee Overview](#Game-overview)
    - [Card Setup](#card-setup)
    - [Deck Creation](#deck-creation)
    - [Card Dealing](#card-dealing)
    - [Hand Evaluation](#hand-evaluation)
    - [AI Decision-Making](#ai-decision-making)
    - [Betting Mechanics](#betting-mechanics)
    - [Showdown and Winner](#showdown-and-winner)
- [Example Game-Play](#example-game-play)

## Game Features

- **AI Strategy**: Uses **Expectiminimax** decision-making for AI players, evaluating potential outcomes based on poker hand strength, pot odds, and simulation of opponent responses.
- **Multiplayer**: Includes 1 human player and 5 AI players, all participating in poker rounds (pre-flop, flop, turn, river).
- **Game Flow**: Incorporates **community cards** (flop, turn, and river) and **betting rounds** where each player must make strategic decisions.
- **Hand Evaluation**: Determines the best hand from the player’s hand and the community cards, applying standard poker hand rankings.

## How to Run the Game

1. Ensure Python (version 3.x or later) is installed.
2. Clone or download the repository containing this game.
3. Open a terminal/command prompt.
4. Run the script with the following command:
   ```bash
   python pokergame.py
5. The game will start in the terminal, displaying your cards and the community cards. Follow the prompts to make your decisions.

## Methodology

The game leverages **Expectiminimax** decision-making for AI behavior, allowing AI players to consider not only their hand strength but also the likelihood of winning based on the remaining community cards and their current bet. This approach helps in making strategic decisions such as folding, betting, calling, and raising.

## Game Flow

1. **Dealing**: Each player receives 2 hole cards. The dealer also prepares 5 community cards which will be revealed in stages.

2. **Betting Rounds**: Players (human and AI) take turns betting after the **pre-flop**, **flop**, **turn**, and **river**.

3. **Showdown**: After the final betting round, the player with the best 5-card hand (using their hole cards and community cards) wins the pot.

## Game Overview

### **Card Setup**
Defines the suits and ranks of the deck, and sets up the possible hand rankings in poker.

   ``bash
   SUITS = ['Hearts', 'Diamonds', 'Clubs', 'Spades']
   RANKS = ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A']
   HAND_RANKS = 'High Card', 'One Pair', 'Two Pair', 'Three of a Kind', 'Straight', 'Flush', 'Full House', 'Four of a Kind', 'Straight Flush', 'Royal Flush'

### **Deck Creation**
The deck is created as a standard 52-card deck.

   ```bash
   def create_deck():
   return [(rank, suit) for suit in SUITS for rank in RANKS]
```
### **Shuffling the Deck**
The deck is shuffled using Python's `random.shuffle` method to randomize the card order before dealing.

   ```python
   def shuffle_deck(deck):
   random.shuffle(deck)
```
### **Card Dealing**
Cards are dealt to players, ensuring each player receives two cards (hole cards). Community cards are later dealt in stages.

   ```python
   def deal_cards(deck, num_players=6):
   hands = {f'Player {i+1}': [] for i in range(num_players)}  # Players 1 to 6
   for i in range(num_players):
   hands[f'Player {i+1}'].append(deck.pop())
   hands[f'Player {i+1}'].append(deck.pop())
   return hands, deck
```
### **Hand Evaluation**
The hand strength is determined using a series of helper functions that evaluate flushes and straights. The function `evaluate_hand()` returns the best possible hand from the player's cards and the community cards.

   ```python
   def evaluate_hand(cards):
    values = [card[0] for card in cards]
    counts = Counter(values)
    flush = is_flush(cards)
    straight = is_straight(cards)
    if straight and flush:
        if 'A' in values and 'K' in values:
            return "Royal Flush"
        return "Straight Flush"
    if 4 in counts.values():
        return "Four of a Kind"
    if 3 in counts.values() and 2 in counts.values():
        return "Full House"
    if flush:
        return "Flush"
    if straight:
        return "Straight"
    if 3 in counts.values():
        return "Three of a Kind"
    if list(counts.values()).count(2) == 2:
        return "Two Pair"
    if 2 in counts.values():
        return "One Pair"
    return "High Card"
```
### **AI Decision-Making**
The **Expectiminimax** algorithm is used to make decisions for the AI players. It simulates the AI’s potential decisions based on the current game state and evaluates the best course of action for each possible outcome.

```python
def expectiminimax_decision(hand, community_cards, deck, current_bet, pot, depth=2):
    def simulate_opponent_response(ai_strength, odds):
        if ai_strength > 6:
            return ['call', 'raise']
        elif ai_strength > 3:
            return ['call', 'fold']
        else:
            return ['fold', 'bluff'] if odds > 0.3 else ['call']

def evaluate_terminal(hand, community_cards):
        full_hand = hand + community_cards
        strength = evaluate_hand(full_hand)
        values = {
            "High Card": 1, "One Pair": 2, "Two Pair": 3, "Three of a Kind": 4,
            "Straight": 5, "Flush": 6, "Full House": 7, "Four of a Kind": 8,
            "Straight Flush": 9, "Royal Flush": 10
        }
        return values[strength]
```
### **Betting Mechanism**
The game includes a betting round function where players can choose to fold, call, raise, or check. The AI players make decisions based on their hand and current pot odds.

### **Showdown and Winner**
After the betting rounds, the winner is determined based on the best hand from the player and community cards.

```python
print("\n--- Showdown ---")
    hand_values = {
        "Royal Flush": 10, "Straight Flush": 9, "Four of a Kind": 8, "Full House": 7,
        "Flush": 6, "Straight": 5, "Three of a Kind": 4, "Two Pair": 3, "One Pair": 2, "High Card": 1
    }
    print("Community Cards:", community_cards)
    print("\nPlayer Hands and Evaluations:")
    highest_strength = -1
    winner = ""
    best_hand = ""

    for player, hand in hands.items():
        full_hand = hand + community_cards
        hand_strength = evaluate_hand(full_hand)
        strength = hand_values[hand_strength]
        print(f"{player}: {hand} -> {hand_strength}")
        if strength > highest_strength:
            highest_strength = strength
            best_hand = hand_strength
            winner = player

    print(f"\nThe winner is {winner} with a {best_hand}!")
    play_again = input("\nDo you want to play again? (yes/no): ").lower()
    if play_again == "yes":
        play_game()
    else:
        print("Thank you for playing!")
        exit()
```
### **Rounds in Game-Play**
<img src="D:\Downloads\STUDYmaterials\440\Texas Hold'em Poker/poker-game.png" alt="Poker Image" width="300"/>

![Poker Image](D:\Downloads\STUDYmaterials\440\Texas Hold'em Poker/poker-game.png)
### 1. Pre-flop Betting Round

### 2. AI Actions Displayed

### 3. Showdown

### 4. Replay Option

## Conclusion

This **Texas Hold'em Poker** game uses **AI** to simulate strategic decisions using the **Expectiminimax** algorithm. It is designed for **text-based interaction** and allows the player to experience poker against **AI opponents** who make realistic decisions based on the current game state.
