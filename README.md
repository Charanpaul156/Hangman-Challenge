# Hangman-Challenge
import random

def choose_word():
    words = ["python", "hangman", "challenge", "programming", "developer"]
    return random.choice(words)

def display_hangman(tries):
    stages = [
        """
           ------
           |    |
           |    O
           |   /|\\
           |   / \\
           |
        """,
        """
           ------
           |    |
           |    O
           |   /|\\
           |   /
           |
        """,
        """
           ------
           |    |
           |    O
           |   /|
           |
           |
        """,
        """
           ------
           |    |
           |    O
           |    |
           |
           |
        """,
        """
           ------
           |    |
           |    O
           |
           |
           |
        """,
        """
           ------
           |    |
           |
           |
           |
           |
        """,
        """
           ------
           |
           |
           |
           |
           |
        """
    ]
    return stages[tries]

def hangman():
    word = choose_word()
    guessed = ['_'] * len(word)
    guessed_letters = set()
    tries = 6

    print("Welcome to Hangman!")
    
    while tries > 0 and '_' in guessed:
        print(display_hangman(tries))
        print("Word: " + ' '.join(guessed))
        print("Guessed Letters: " + ' '.join(sorted(guessed_letters)))
        
        guess = input("Guess a letter: ").lower()
        
        if guess in guessed_letters:
            print("You already guessed that letter. Try again.")
        elif guess in word:
            print("Good guess!")
            for index, letter in enumerate(word):
                if letter == guess:
                    guessed[index] = guess
            guessed_letters.add(guess)
        else:
            print("Wrong guess!")
            guessed_letters.add(guess)
            tries -= 1

    if '_' not in guessed:
        print("Congratulations! You've guessed the word:", word)
    else:
        print(display_hangman(tries))
        print("Sorry, you ran out of tries. The word was:", word)

if __name__ == "__main__":
    hangman()
