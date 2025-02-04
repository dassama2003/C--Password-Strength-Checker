# C--Password-Strength-Checker
#include <iostream>
#include <cctype>
#include <vector>

using namespace std;

// Common weak passwords
vector<string> weakPasswords = {"password", "123456", "qwerty", "letmein", "12345678"};

// Function to check if password is in weak list
bool isWeakPassword(const string &password) {
    for (const string &weak : weakPasswords) {
        if (password == weak) {
            return true;
        }
    }
    return false;
}

// Function to check password strength
string checkPasswordStrength(const string &password) {
    if (password.length() < 8) {
        return "Weak (Too Short)";
    }

    bool hasUpper = false, hasLower = false, hasDigit = false, hasSpecial = false;

    for (char ch : password) {
        if (isupper(ch)) hasUpper = true;
        else if (islower(ch)) hasLower = true;
        else if (isdigit(ch)) hasDigit = true;
        else hasSpecial = true;
    }

    if (isWeakPassword(password)) {
        return "Weak (Common Password)";
    }

    if (hasUpper && hasLower && hasDigit && hasSpecial) {
        return "Strong";
    } else if ((hasUpper || hasLower) && hasDigit) {
        return "Medium";
    }

    return "Weak";
}

int main() {
    string password;
    cout << "Enter a password: ";
    cin >> password;

    string strength = checkPasswordStrength(password);
    cout << "Password Strength: " << strength << endl;

    return 0;
}
