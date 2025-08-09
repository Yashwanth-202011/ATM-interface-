# ATM-interface-
It is an ATM interface in which we are able to check balance, deposit or withdrawal of money and also can create a new account.

#include <iostream>
using namespace std;

class ATM {
public:
    int balance;
    string name;

    ATM(int bal, string name) : balance(bal), name(name) {}

    void check_balance() {
        cout << "Your bank balance is " << balance << endl;
    }

    void deposit(int amount) {
        balance += amount;
        cout << "Amount deposited to your account." << endl;
    }

    void withdraw(int amount) {
        if (amount > balance) {
            cout << "Insufficient balance." << endl;
        } else {
            balance -= amount;
            cout << "Amount debited from your account." << endl;
        }
    }
};

int main() {
    ATM* customers[20] = { nullptr };  // initialize all pointers to nullptr
    int option;

    while (true) {
        cout << "\nSelect an option:\n"
             << "1. Check balance\n"
             << "2. Deposit\n"
             << "3. Withdraw\n"
             << "4. Create account\n"
             << "5. Exit\n"
             << "Enter your choice (1-5): ";
        cin >> option;

        if (option == 5) {
            cout << "Exiting program." << endl;
            break;
        }

        int accno;
        switch (option) {
            case 1:
                cout << "Enter your account number (0-19): ";
                cin >> accno;
                if (accno < 0 || accno >= 20 || customers[accno] == nullptr) {
                    cout << "Invalid or non-existent account number." << endl;
                } else {
                    customers[accno]->check_balance();
                }
                break;

            case 2:
                cout << "Enter your account number (0-19): ";
                cin >> accno;
                if (accno < 0 || accno >= 20 || customers[accno] == nullptr) {
                    cout << "Invalid or non-existent account number." << endl;
                } else {
                    int amount;
                    cout << "Enter amount to deposit: ";
                    cin >> amount;
                    customers[accno]->deposit(amount);
                }
                break;

            case 3:
                cout << "Enter your account number (0-19): ";
                cin >> accno;
                if (accno < 0 || accno >= 20 || customers[accno] == nullptr) {
                    cout << "Invalid or non-existent account number." << endl;
                } else {
                    int amount;
                    cout << "Enter amount to withdraw: ";
                    cin >> amount;
                    customers[accno]->withdraw(amount);
                }
                break;

            case 4:
                cout << "Enter new account number (0-19): ";
                cin >> accno;
                if (accno < 0 || accno >= 20) {
                    cout << "Invalid account number." << endl;
                } else if (customers[accno] != nullptr) {
                    cout << "Account already exists." << endl;
                } else {
                    string name;
                    int balance;
                    cout << "Enter account holder name: ";
                    cin.ignore();  // clear newline from input buffer
                    getline(cin, name);
                    cout << "Enter initial balance: ";
                    cin >> balance;
                    customers[accno] = new ATM(balance, name);
                    cout << "Account created successfully!\n";
                }
                break;
            default:
                cout << "Invalid option! Please select between 1 and 5." << endl;
        }
    }

    // Clean up dynamically allocated memory before program ends
    for (int i = 0; i < 20; i++) {
        delete customers[i];
    }

    return 0;
}
