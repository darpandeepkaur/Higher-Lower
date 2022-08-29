from art import logo, vs
import random
from game_data import data
from replit import clear

def random_account():
  return random.choice(data)

def format_data(account):
  name = account["name"]
  description = account["description"]
  country= account["country"]

  return f"{name}, {description}, from {country}"

def check_answer(guess, account_a_followers, account_b_followers):
  if account_a_followers > account_b_followers:
    return guess == "a"
  else:
    return guess == "b"
  

def game():
  print(logo)
  score = 0
  should_continue = True
  
  account_a = random_account()
  account_b = random_account()

  
  while should_continue:
    account_a = account_b
    account_b = random_account()

    while account_a == account_b:
      account_b = random_account()
      
    print(f"Compair A: {format_data(account_a)}")
    print(vs)
    print(f"Against B: {format_data(account_b)}")
  
    guess = input("Who has more followers? Type 'A' or 'B': ").lower()
    is_correct = check_answer(guess, account_a["follower_count"], account_b["follower_count"])
  
    clear()
    print(logo)
    
    if is_correct:
      score += 1
      print(f"You're right! Current score: {score}")
    else:
      should_continue = False
      print(f"Sorry, that's wrong. Final score: {score}")
      

  
game()
