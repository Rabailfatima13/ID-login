# ID-login
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

class User {
public:
    string username;
    string password;

    bool registerUser() {
        cout << "Enter a username: ";
        cin >> username;
        cout << "Enter a password: ";
        cin >> password;

        ofstream file;
        file.open("database.txt", ios::app);

        if (file.is_open()) {
            file << username << " " << password << endl;
            file.close();
            cout << "Registration successful!\n";
            return true;
        } else {
            cout << "Failed to open the database file.\n";
            return false;
        }
    }

    bool loginUser() {
        cout << "Enter your username: ";
        cin >> username;
        cout << "Enter your password: ";
        cin >> password;

        ifstream file("database.txt");
        string u, p;
        bool loginSuccess = false;

        if (file.is_open()) {
            while (file >> u >> p) {
                if (u == username && p == password) {
                    loginSuccess = true;
                    break;
                }
            }
            file.close();

            if (loginSuccess) {
                cout << "Login successful!\n";
                return true;
            } else {
                cout << "Invalid username or password.\n";
                return false;
            }
        } else {
            cout << "Failed to open the database file.\n";
            return false;
        }
    }
};

int main() {
    User user;
    int choice;

    cout << "Welcome to the Login and Registration System!\n";
    cout << "1. Register\n";
    cout << "2. Login\n";
    cout << "3. Exit\n";

    cout << "Enter your choice: ";
    cin >> choice;

    switch (choice) {
    case 1:
        if (user.registerUser()) {
            cout << "You can now log in with your credentials.\n";
        }
        break;
    case 2:
        user.loginUser();
        break;
    case 3:
        cout << "Exiting the system. Goodbye!\n";
        break;
    default:
        cout << "Invalid choice. Please try again.\n";
        break;
    }

    return 0;
}
