"""A small console Hangman game."""

import random

WORDS = ["python", "coding", "laptop", "planet", "garden"]
MAX_INCORRECT_GUESSES = 6


def display_word(word: str, guessed_letters: set[str]) -> str:
    """Return the word with unguessed letters hidden."""
    return " ".join(letter if letter in guessed_letters else "_" for letter in word)


def choose_word() -> str:
    """Choose one of the predefined words."""
    return random.choice(WORDS)


def play_game() -> None:
    """Run one game of Hangman."""
    word = choose_word()
    guessed_letters: set[str] = set()
    incorrect_guesses = 0

    print("Welcome to Hangman! Guess the word one letter at a time.")
    while incorrect_guesses < MAX_INCORRECT_GUESSES:
        print(f"\nWord: {display_word(word, guessed_letters)}")
        print(f"Incorrect guesses left: {MAX_INCORRECT_GUESSES - incorrect_guesses}")
        guess = input("Enter one letter: ").strip().lower()

        if len(guess) != 1 or not guess.isalpha():
            print("Please enter exactly one letter.")
            continue
        if guess in guessed_letters:
            print("You already guessed that letter.")
            continue

        guessed_letters.add(guess)
        if guess in word:
            print("Correct!")
        else:
            incorrect_guesses += 1
            print("That letter is not in the word.")

        if all(letter in guessed_letters for letter in word):
            print(f"\nYou won! The word was '{word}'.")
            return

    print(f"\nGame over. The word was '{word}'.")


if __name__ == "__main__":
    play_game()
