import time

# Welcome message
print("Welcome to the Python Vending Machine.")

# Asking the user how much money they wish to insert.
while True:
    try:
        number_of_Dhs = int(input("How many Dhs would you like to insert? "))
        if number_of_Dhs < 0:
            print("Please enter a positive amount.")
            continue
        break
    except ValueError:
        print("Invalid input. Please enter a valid number.")

# Creating a variable to store the total amount of money inserted into the vending machine.
change = round(number_of_Dhs, 2)

# Informing the user of how much they have entered in total.
print(f"\nIn total you have entered Dhs {change}")
time.sleep(2)

# Dictionary for product names and prices
products = {
    "candy": 3,
    "Coke": 5,
    "Mountain Dew": 4,
    "Water Bottle": 1,
    "tshirts": 20,
    "teddy bear": 5,
    "plushie": 15,
    "shoes": 60,
    "pokemon cards": 4,
    "Pepsi": 2.50,
    "books": 9.50,
    "cards": 4,
    "gift card": 12,
    "albums": 15,
}

# Dictionary to track the number of each product bought
products_bought = {product: 0 for product in products}

# Informing the user of the choices available and their prices
print("\nAvailable products and prices:")
for product, price in products.items():
    print(f"{product}: Dhs {price}")

print()

# Main loop where user can choose products
while change > 0:
    customer_choice = input("What would you like to buy? Type 'N' when you are finished: ").strip()

    if customer_choice.lower() == 'n':
        print("\nTransaction details:")
        print("You purchased:")
        for product, quantity in products_bought.items():
            if quantity > 0:
                print(f"{product} x {quantity}")
        print(f"You have Aed {change} remaining.")
        break

    if customer_choice in products:
        product_price = products[customer_choice]
        if change >= product_price:
            # Decrease the money and update purchase count
            change -= product_price
            products_bought[customer_choice] += 1
            change = round(change, 2)
            print(f"You have chosen a {customer_choice}. This costs Aed {product_price}.")
            print(f"Remaining balance: Dhs {change}")
        else:
            print(f"Insufficient funds. You need Dhs {product_price}, but you only have Dhs {change}.")
    else:
        print("Invalid selection. Please choose a valid product.")

    time.sleep(1)

# If out of money, exit the loop
if change <= 0:
    print("\nYou have run out of money.")
    print("\nTransaction details:")
    print("You purchased:")
    for product, quantity in products_bought.items():
        if quantity > 0:
            print(f"{product} x {quantity}")
    print(f"You have Dhs {change} remaining.")
