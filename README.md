#include <iostream>
#include <vector>
#include <fstream>

using namespace std;

struct Contact {
    string name, phone, email;
};

vector<Contact> contacts;

void addContact() {
    Contact c;
    cout << "Имя: "; cin >> c.name;
    cout << "Телефон: "; cin >> c.phone;
    cout << "Email: "; cin >> c.email;
    contacts.push_back(c);
}

void listContacts() {
    if (contacts.empty()) cout << "Список пуст!\n";
    for (size_t i = 0; i < contacts.size(); i++)
        cout << i + 1 << ". " << contacts[i].name << " " << contacts[i].phone << " " << contacts[i].email << endl;
}

void searchContact() {
    string name;
    cout << "Введите имя Любое: ";
    cin >> name;
    for (auto& c : contacts)
        if (c.name == name)
            cout << c.name << " " << c.phone << " " << c.email << endl;
}

void deleteContact() {
    int index;
    listContacts();
    cout << "Введите номер для удаления: ";
    cin >> index;
    if (index > 0 && index <= contacts.size())
        contacts.erase(contacts.begin() + index - 1);
}

void editContact() {
    int index;
    listContacts();
    cout << "Введите номер для изменения: ";
    cin >> index;
    if (index > 0 && index <= contacts.size()) {
        cout << "Новое имя люьое : "; cin >> contacts[index - 1].name;
        cout << "Новый телефон: "; cin >> contacts[index - 1].phone;
        cout << "Новый email: "; cin >> contacts[index - 1].email;
    }
}

void saveToFile() {
    ofstream file("contacts.txt");
    for (auto& c : contacts)
        file << c.name << " " << c.phone << " " << c.email << endl;
}

void loadFromFile() {
    ifstream file("contacts.txt");
    Contact c;
    while (file >> c.name >> c.phone >> c.email)
        contacts.push_back(c);
}

int main() {
    setlocale(LC_ALL, "RU");
    loadFromFile();
    int choice;
    do {
        cout << "\n1. Добавить\n2. Список\n3. Поиск\n4. Удалить\n5. Изменить\n6. Сохранить\n7. Выйти\nВыбор: ";
        cin >> choice;
        if (choice == 1) addContact();
        else if (choice == 2) listContacts();
        else if (choice == 3) searchContact();
        else if (choice == 4) deleteContact();
        else if (choice == 5) editContact();
        else if (choice == 6) saveToFile();
    } while (choice != 7);
}

