import random
import sys
import os

print("\n\n   **************                       Hello!                 **************   ")
print("   *************               Welcome to the ATM Banking      **************   \n")
print("   *************  In This pre-define program  your PIN Number  **************     ")
print("   *************                    Pin Number is: 1998        **************     ")
print("________________________________________________________________________________\n")


# declaration of class
class Atm:
    def __init__(self, holder_name, ac_number, balance=1000, pin_numbers=1998):
        self.name = holder_name
        self.account_number = ac_number
        self.amount = None
        self.balance = balance
        self.pin_number = pin_numbers

    # function to verify the pin is wright or wrong
    def verify_pin(self, pin_no):
        print(f"\n\n pin_no:%s" % pin_no)
        file1 = open("PinData.txt", "w")
        file1.write(str(pin_no))
        file1.close()
        if self.pin_number == int(pin_no):
            print(" Congratulations! Account created successfully......\n")
            print("successfully verified your pin_number")
            print("you can login to your Account")

        else:
            print(" You entered wrong pin number ")
            print(" PLEASE ENTER VALID PIN NUMBER")
            sys.exit()

    # function to display the Account detail in the menu
    def account_detail(self):
        print("\n----------ACCOUNT DETAIL----------")
        print(f"Account Holder: {self.name.upper()}")
        print(f"Account Number: {self.account_number}")
        print(f"Available balance: RS.{self.balance}\n")

    # function to deposit the money to the Atm bank
    def deposit(self, amount):
        self.amount = amount
        self.balance = self.balance + self.amount
        print("Current account balance: RS.", self.balance)
        print()

    # function to clear the output of screen in Atm bank menu page
    def clearscreen(self):
        os.system('clear')
        # print blank line after clearing the screen
        print()

    # function to withdraw the amount from the atm banking
    def withdraw(self, amount):
        self.amount = amount
        if self.amount > self.balance:
            print("You don't have enough money in your Account")
            print(f"Your Current balance is RS.{self.balance} only.")
            print("Please contact to your Bank Customer Services")
            print()
        else:
            self.balance = self.balance - self.amount
            print(f"RS.{amount} withdrawal successful!")
            print("Your Current account balance: RS.", self.balance)
            print()

    # function to check the remaining balance in the ATM bank
    def check_balance(self):
        print("\n Currently Users Available balance: RS.", self.balance)
        print()

    # function to display the Menu for transaction
    def transaction(self):
        print("""
            Menu:
        $$$$$$$$$$$$$$$$$$$$$$
            Options:
            1. Account Detail
            2. Check Balance
            3. Deposit Cash
            4. Withdraw Cash
            5. Exit
        $$$$$$$$$$$$$$$$$$$$$$$
        """)

        while True:
            try:
                option = int(input("Choose your Option from "
                                   "1, 2, 3, 4 or 5:"))
            except Exception:
                print("Error!"
                      "Please Choose your option from 1, 2, 3, 4, or 5 only!\n")
                continue
            else:
                if option == 1:
                    atm.account_detail()
                elif option == 2:
                    atm.check_balance()
                elif option == 3:
                    amount = int(input(""
                                       ""
                                       "\nYou have choose to Deposit money\n"
                                       "How much you want to deposit(RS.):"))
                    atm.deposit(amount)
                elif option == 4:
                    amount = int(input(""
                                       ""
                                       "\nYou have choose to Deposit money\n"
                                       "How much you want to withdraw(RS.):"))
                    atm.withdraw(amount)
                elif option == 5:
                    print(f"""
                printing receipt..............
          ******************************************
              Transaction is now complete.                         
              Transaction number: {random.randint(10000, 1000000)} 
              Account holder: {self.name.upper()}                  
              Account number: {self.account_number}                
              Available balance: RS.{self.balance}                    

          ******************************************
          """)
                    print("---------------Take your receipt!!!--------------------")
                    print("-----Thank you for Choosing ATM Banking Machine!!!-----")
                    print("""
                                $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

                                          Visit us again!               

                                $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$
                                    """)
                    sys.exit()


def main():
    print("-------------------------------------------------------------")


print("------------------------------Account Creation in ATM Bank--------------------------------")
name = input("Enter your name: ")
file = open("Pin_data.txt", "w")
file.write(name)
file.close()
account_number = input("Enter your account number: ")
file = open("Pin_data.txt", "w")
file.write(account_number)
file.close()
pin_number = input("Enter your pin number: ")

atm = Atm(name, account_number)

while True:
    atm.verify_pin(pin_number)
    login = input("Do you want to login to your account?(y/n):")
    if login == "y":
        atm.transaction()
    elif login == "n":

        print("---------------Take your receipt!!!--------------------")
        print("-----Thank you for Choosing ATM Banking Machine!!!-----")
        print("""
            $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

                      Visit us again!               

            $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$
                """)
        break
    else:
        print("Wrong command!  Enter 'y' for yes and 'n' for NO.\n")

if __name__ == "__main__":
    main()

