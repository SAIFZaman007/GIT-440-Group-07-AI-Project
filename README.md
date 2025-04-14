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
