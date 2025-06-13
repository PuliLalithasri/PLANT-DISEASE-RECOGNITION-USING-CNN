import random
import time
import os

# ASCII Art for Rock, Paper, Scissors
ascii_art = {
    "rock": '''
        _______
    ---'   ____)
          (_____)
          (_____)
          (____)
    ---.__(___)
    ''',
    "paper": '''
         _______
    ---'    ____)____
               ______)
              _______)
             _______)
    ---.__________)
    ''',
    "scissors": '''
        _______
    ---'   ____)____
              ______)
           __________)
          (____)
    ---.__(___)
    '''
}

# Add color for terminal output
class Colors:
    HEADER = '\033[95m'
    OKBLUE = '\033[94m'
    OKCYAN = '\033[96m'
    OKGREEN = '\033[92m'
    WARNING = '\033[93m'
    FAIL = '\033[91m'
    ENDC = '\033[0m'
    BOLD = '\033[1m'

# Clear screen function for cleaner interface
def clear_screen():
    os.system('cls' if os.name == 'nt' else 'clear')

# Game logic
def determine_winner(user, computer):
    if user == computer:
        return "draw"
    elif (user == "rock" and computer == "scissors") or \
         (user == "paper" and computer == "rock") or \
         (user == "scissors" and computer == "paper"):
        return "user"
    else:
        return "computer"

# Main game loop
def play_game():
    choices = ["rock", "paper", "scissors"]

    clear_screen()
    print(f"{Colors.HEADER}{Colors.BOLD}🎮 Welcome to Rock, Paper, Scissors! 🎮{Colors.ENDC}\n")

    while True:
        print(f"{Colors.OKBLUE}Choose one:{Colors.ENDC}")
        for i, choice in enumerate(choices, 1):
            print(f"{i}. {choice.capitalize()}")

        try:
            user_input = int(input("\nEnter the number of your choice (1-3): "))
            if user_input not in [1, 2, 3]:
                raise ValueError
            user_choice = choices[user_input - 1]
        except ValueError:
            print(f"{Colors.FAIL}Invalid input! Please enter a number between 1 and 3.{Colors.ENDC}")
            continue

        computer_choice = random.choice(choices)

        # Show choices with dramatic effect
        print(f"\n{Colors.WARNING}Rock...")
        time.sleep(0.5)
        print("Paper...")
        time.sleep(0.5)
        print("Scissors... Shoot!{Colors.ENDC}\n")
        time.sleep(0.5)

        print(f"{Colors.OKCYAN}You chose:{Colors.ENDC}")
        print(ascii_art[user_choice])
        print(f"{Colors.OKCYAN}Computer chose:{Colors.ENDC}")
        print(ascii_art[computer_choice])

        winner = determine_winner(user_choice, computer_choice)
        if winner == "draw":
            print(f"{Colors.WARNING}It's a draw! 🤝{Colors.ENDC}")
        elif winner == "user":
            print(f"{Colors.OKGREEN}You win! 🎉{Colors.ENDC}")
        else:
            print(f"{Colors.FAIL}Computer wins! 💻{Colors.ENDC}")

        # Ask to play again
        again = input(f"\n{Colors.BOLD}Do you want to play again? (y/n): {Colors.ENDC}").lower()
        if again != 'y':
            print(f"\n{Colors.OKBLUE}Thanks for playing! Goodbye! 👋{Colors.ENDC}")
            break
        clear_screen()

# Run the game
if __name__ == "__main__":
    play_game()
