# phase-2
experiential learning
import random

# ==========================================
# NUMBER GUESSING GAME - PHASE 2
# ==========================================

def display_welcome():
    print("=" * 50)
    print("       🎯 NUMBER GUESSING GAME")
    print("=" * 50)
    print("Welcome to the Number Guessing Game!")
    print("Try to guess the secret number.")
    print("You will get hints after every wrong guess.")
    print("=" * 50)


def choose_difficulty():
    print("\nChoose Difficulty Level:")
    print("1. Easy   (1 - 50, 10 attempts)")
    print("2. Medium (1 - 100, 7 attempts)")
    print("3. Hard   (1 - 200, 5 attempts)")

    while True:
        choice = input("\nEnter your choice (1/2/3): ")

        if choice == "1":
            return 50, 10, "Easy"
        elif choice == "2":
            return 100, 7, "Medium"
        elif choice == "3":
            return 200, 5, "Hard"
        else:
            print("Invalid choice! Please enter 1, 2, or 3.")


def calculate_score(attempts_left, total_attempts, difficulty):
    base_score = attempts_left * 10

    if difficulty == "Easy":
        bonus = 10
    elif difficulty == "Medium":
        bonus = 20
    else:
        bonus = 30

    return base_score + bonus


def give_hint(number, guess):
    difference = abs(number - guess)

    if difference <= 5:
        print("🔥 Very close!")
    elif difference <= 15:
        print("😊 You are close!")
    elif difference <= 30:
        print("🙂 You are a little far.")
    else:
        print("🥶 You are far away.")


def play_game():
    max_number, max_attempts, difficulty = choose_difficulty()

    secret_number = random.randint(1, max_number)
    attempts_left = max_attempts
    guesses = []

    print("\n" + "-" * 50)
    print("Difficulty:", difficulty)
    print("Guess a number between 1 and", max_number)
    print("Total attempts:", max_attempts)
    print("-" * 50)

    while attempts_left > 0:

        print("\nAttempts left:", attempts_left)

        try:
            guess = int(input("Enter your guess: "))

            if guess < 1 or guess > max_number:
                print("⚠️ Please enter a number within the given range.")
                continue

            if guess in guesses:
                print("⚠️ You already guessed this number!")
                continue

            guesses.append(guess)
            attempts_left -= 1

            if guess == secret_number:
                score = calculate_score(
                    attempts_left,
                    max_attempts,
                    difficulty
                )

                print("\n🎉 CONGRATULATIONS! 🎉")
                print("You guessed the correct number!")
                print("Secret number:", secret_number)
                print("Number of guesses:", len(guesses))
                print("Your score:", score)
                print("=" * 50)

                return True

            elif guess < secret_number:
                print("📈 Too low! Try a higher number.")
                give_hint(secret_number, guess)

            else:
                print("📉 Too high! Try a lower number.")
                give_hint(secret_number, guess)

        except ValueError:
            print("❌ Invalid input! Please enter a number.")

    print("\n😔 GAME OVER!")
    print("You have used all your attempts.")
    print("The correct number was:", secret_number)
    print("Your guesses:", guesses)
    print("=" * 50)

    return False


def show_rules():
    print("\n" + "=" * 50)
    print("              📜 GAME RULES")
    print("=" * 50)
    print("1. The computer selects a random number.")
    print("2. You have limited attempts.")
    print("3. Enter one number at a time.")
    print("4. You will receive HIGH/LOW hints.")
    print("5. Repeated guesses are not allowed.")
    print("6. Your score depends on remaining attempts.")
    print("=" * 50)


def main():
    display_welcome()

    while True:
        print("\nMAIN MENU")
        print("1. Start Game")
        print("2. Game Rules")
        print("3. Exit")

        choice = input("\nEnter your choice: ")

        if choice == "1":
            play_game()

            while True:
                again = input("\nDo you want to play again? (yes/no): ").lower()

                if again == "yes" or again == "y":
                    break

                elif again == "no" or again == "n":
                    print("\nThanks for playing! 👋")
                    return

                else:
                    print("Please enter yes or no.")

        elif choice == "2":
            show_rules()

        elif choice == "3":
            print("\nThanks for playing! 👋")
            break

        else:
            print("❌ Invalid choice! Please select 1, 2, or 3.")


# Start the program
if __name__ == "__main__":
    main()
