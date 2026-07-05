# ATM-SYSTEM-PROGRAM
This project is a simple ATM (Automated Teller Machine) simulation developed in Python. It demonstrates the use of basic programming concepts by allowing a user to interact with an ATM-like menu after entering the correct PIN Check Balance Withdraw Money Deposit Money Exit

balance=0

print("Welcome we are glad to have you here!")
pinCreation= input("Create your 4 digit password: ")
while len(pinCreation) !=4 or not pinCreation.isdigit():
    print(" Please enter a 4 digit password")
    pinCreation= input("Create your 4 digit password: ")
if len(pinCreation) ==4 and pinCreation.isdigit():
    transaction_history=[]

    AskToContinue= input("Will like to continue (y/n)?")
    if AskToContinue=="n":
        print("Thank you for choosing to bannk with us")
    elif AskToContinue == "y":
        print("Now you can login to your account")

        attempt=0
        maxAttempt=3

        askForPin= input("Enter your ATM pin: ")

        while attempt <3:
            if askForPin != pinCreation:
                attempt+=1
                print(f"Attempt left: {maxAttempt-attempt}")
                askForPin= input("Enter your ATM pin: ")
            elif askForPin==pinCreation:

                while True:
                    print("=====ATM MENU=====")
                    print("1. Check Balance")
                    print("2. Deposit")
                    print("3. Withdraw")
                    print("4. Transaction History")
                    print("5. Change Pin")
                    print("6. Exit")

                    askForOption = int(input("Choose an option: "))

                    if askForOption == 1:
                        print(f"Current Balance: {balance}")
                        transaction_history.append(f"Current Balance: {balance}")
                    elif askForOption == 2:
                        askForDepositAmount= int(input("Enter the amount you want to deposite: "))
                        if askForDepositAmount > 0:
                            balance+=askForDepositAmount
                            transaction_history.append(f"Deposite: {askForDepositAmount}")
                            print("Deposite successful")
                        else:
                            print("Deposite failed")
                    elif askForOption == 3:
                        askForWithrawalAmount= int(input("Enter amount: "))
                        askForAtmPin= input("Enter your atm pin: ")
                        if askForAtmPin!= pinCreation:
                            print("Incorrect pin")
                        elif askForAtmPin == pinCreation:
                            if askForWithrawalAmount <= balance:
                                balance-=askForWithrawalAmount
                                print("Withdraw successful")
                                transaction_history.append(f"Withdrawal: {askForWithrawalAmount}")
                            elif askForWithrawalAmount > balance:
                                print("Insufficient fund")
                    elif askForOption == 4:
                        if not transaction_history:
                            print("No transaction yet")
                        else:
                            for transaction in transaction_history:
                                print(transaction)
                    elif askForOption == 5:
                        askForCurrentPin= input("Enter your old pin: ")
                        if askForCurrentPin != pinCreation:
                            print("Incorrect pin")
                            askForCurrentPin= input("Enter your old pin: ")
                        elif askForCurrentPin == pinCreation:
                            askForNewPin= input("Enter your new pin: ")
                            if len(askForNewPin) == 4 and askForNewPin.isdigit():
                                askForConfirmPin= input("Confirm the pin: ")
                                if askForConfirmPin == askForNewPin:
                                    pinCreation= askForConfirmPin
                                    print("Pin change successful")
                                elif askForConfirmPin != askForNewPin:
                                    print("Incorrect pin")
                                    askForNewPin= input("Enter your new pin: ")
                    elif askForOption == 6:
                        print("Thank you for banking with us")
                        break
                break
        if attempt == maxAttempt:
            print("Account Locked")

