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

```bash
SUITS = ['Hearts', 'Diamonds', 'Clubs', 'Spades']
RANKS = ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A']
HAND_RANKS = ['High Card', 'One Pair', 'Two Pair', 'Three of a Kind', 'Straight', 'Flush', 'Full House', 'Four of a Kind', 'Straight Flush', 'Royal Flush']

### **Deck Creation**
The deck is created as a standard 52-card deck.

```python
def create_deck():
    return [(rank, suit) for suit in SUITS for rank in RANKS]

## Shuffling the Deck
The deck is shuffled using Python's `random.shuffle` method to randomize the card order before dealing.

```python
def shuffle_deck(deck):
    random.shuffle(deck)

## Card Dealing
Cards are dealt to players, ensuring each player receives two cards (hole cards). Community cards are later dealt in stages.

```python
def deal_cards(deck, num_players=6):
    hands = {f'Player {i+1}': [] for i in range(num_players)}  # Players 1 to 6
    for i in range(num_players):
        hands[f'Player {i+1}'].append(deck.pop())
        hands[f'Player {i+1}'].append(deck.pop())
    return hands, deck
