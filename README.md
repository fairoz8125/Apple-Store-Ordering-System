# Apple-Store-Ordering-System
“Python project for ordering Apple products”

# ================================
#   Apple Store - Product Ordering
# ================================

# Define all Apple products with prices
products = {
    'iphone 11(64GB)': 39999, 'iphone 11(128GB)': 44999, 'iphone 11(256GB)': 49999,
    'iphone 12(64GB)': 51999, 'iphone 12(128GB)': 57999, 'iphone 12(256GB)': 63999,
    'iphone 12 Pro(128GB)': 89900, 'iphone 12 Pro(256GB)': 99900, 'iphone 12 Pro Max(128GB)': 109900,
    'iphone 13(128GB)': 62999, 'iphone 13(256GB)': 69999, 'iphone 13(512GB)': 79999,
    'iphone 13 Pro(128GB)': 99900, 'iphone 13 Pro Max(128GB)': 119900,
    'iphone 14(128GB)': 69999, 'iphone 14(256GB)': 79999, 'iphone 14(512GB)': 89999,
    'iphone 14 Plus(128GB)': 79999, 'iphone 14 Pro(128GB)': 119900, 'iphone 14 Pro Max(128GB)': 139900,
    'iphone 15(128GB)': 74999, 'iphone 15(256GB)': 84999, 'iphone 15(512GB)': 94999,
    'iphone 15 Plus(128GB)': 84999, 'iphone 15 Pro(128GB)': 134900, 'iphone 15 Pro Max(256GB)': 154900,
    'iphone 16(128GB)': 51999, 'iphone 16(256GB)': 78999, 'iphone 16(512GB)': 99900,
    'iphone 16 pro': 119900, 'iphone 16 pro max': 144900,
    'iphone 17(256GB)': 82900, 'iphone 17(512GB)': 102900,
    'iphone 17 Air(256GB)': 119900, 'iphone 17 Air(512GB)': 139900, 'iphone 17 Air(1TB)': 159900,
    'iphone 17 pro(256GB)': 134900, 'iphone 17 pro(512GB)': 154900, 'iphone 17 pro(1TB)': 174900,
    'iphone 17 pro max(256GB)': 149900, 'iphone 17 pro max(512GB)': 169900,
    'iphone 17 pro max(1TB)': 189900, 'iphone 17 pro max(2TB)': 229900,
    'Charger': 2499, 'Cable': 1499, 'Back Cover': 999, 'Temper Glass': 499,
    'MacBook Air M3': 109900, 'MacBook Pro M3': 169900, 'MacBook Pro M3 Max': 249900,
    'iPad (10th Gen)': 44900, 'iPad Air (M2)': 59900, 'iPad Pro (M4)': 99900,
    'Apple Watch SE': 29900, 'Apple Watch Series 10': 45900, 'Apple Watch Ultra 2': 89900,
    'AirPods 3rd Gen': 19900, 'AirPods Pro 2nd Gen': 24900, 'AirPods Max': 59900,
    'HomePod': 32900, 'HomePod Mini': 9900, 'Apple TV 4K': 14900
}

print("WELCOME TO APPLE STORE")

# Display all products
print("\nAvailable Products:")
for item, price in products.items():
    print(f"{item}: RS {price}")

cart = []
order_total = 0

# Helper functions
def normalize(text):
    return text.strip().lower()

# Ordering loop
while True:
    user_input = input("\nEnter the product you want to order (or type 'exit' to finish): ").strip()
    if user_input.lower() == "exit":
        break

    norm_input = normalize(user_input)

    # Find all matching products
    matches = [key for key in products.keys() if norm_input in key.lower()]

    if not matches:
        print(f"❌ Sorry, '{user_input}' is not available!")
        continue

    # If multiple matches, show options
    if len(matches) > 1:
        print("\nMultiple options found:")
        for i, option in enumerate(matches, start=1):
            print(f"{i}. {option}: RS {products[option]}")

        while True:
            choice = input("Enter the number or name of the product you want to add: ").strip()

            # Case 1: User enters a number
            if choice.isdigit() and 1 <= int(choice) <= len(matches):
                selected_product = matches[int(choice)-1]
                break

            # Case 2: User enters the full product name (any case)
            for option in matches:
                if choice.lower() == option.lower():
                    selected_product = option
                    break
            else:
                print("Invalid choice, please enter a valid number or product name.")
                continue
            break
    else:
        selected_product = matches[0]

    # Add to cart
    cart.append(selected_product)
    order_total += products[selected_product]
    print(f"✅ {selected_product} has been added to your order")

# Final Bill
print("\n🛒 Your Cart:")
for c in cart:
    print(f"- {c}: RS {products[c]}")

print(f"\n💰 Total amount to pay: RS {order_total}")
print("\n🙏 Thank you for shopping with Apple Store! ✨")
