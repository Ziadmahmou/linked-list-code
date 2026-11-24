#include <iostream>
#include <string>   
using namespace std;

struct Policy {
    int id;
    string holder;
    string type;
    double coverage;
    Policy* next;
};

// ---------- Linked list ----------
class PolicyList {
    Policy* head;
    int count;

public:
    PolicyList() {
        head = NULL;
        count = 0;
    }

    ~PolicyList() {
        while (head != NULL) {
            Policy* temp = head;
            head = head->next;
            delete temp;
        }
    }

    bool isEmpty() { return head == NULL; }
    int size() { return count; }

    // Find a policy by ID (returns NULL if not found)
    Policy* search(int id) {
        Policy* cur = head;
        while (cur != NULL) {
            if (cur->id == id) return cur;
            cur = cur->next;
        }
        return NULL;
    }

    // Insert at the end
    void insert(int id, string holder, string type, double coverage) {
        if (search(id) != NULL) {
            cout << "Error: this policy ID already exists.\n";
            return;
        }
        Policy* n = new Policy;
        n->id = id;
        n->holder = holder;
        n->type = type;
        n->coverage = coverage;
        n->next = NULL;

        if (head == NULL) {
            head = n;
        }
        else {
            Policy* cur = head;
            while (cur->next != NULL) cur = cur->next;
            cur->next = n;
        }
        count++;
        cout << "Policy added.\n";
    }

    // Delete by ID
    void remove(int id) {
        if (head == NULL) {
            cout << "List is empty.\n";
            return;
        }
        // Case 1: the policy is the first node
        if (head->id == id) {
            Policy* temp = head;
            head = head->next;
            delete temp;
            count--;
            cout << "Policy deleted.\n";
            return;
        }
        // Case 2: the policy is in the middle or the end
        Policy* cur = head;
        while (cur->next != NULL && cur->next->id != id) {
            cur = cur->next;
        }
        if (cur->next == NULL) {
            cout << "Policy not found.\n";
            return;
        }
        Policy* temp = cur->next;
        cur->next = temp->next;
        delete temp;
        count--;
        cout << "Policy deleted.\n";
    }

    // Show one policy
    void show(int id) {
        Policy* p = search(id);
        if (p == NULL) {
            cout << "Policy not found.\n";
            return;
        }
        cout << "ID: " << p->id << " | Holder: " << p->holder
            << " | Type: " << p->type << " | Coverage: " << p->coverage << "\n";
    }

    // Show all policies
    void display() {
        if (head == NULL) {
            cout << "No policies yet.\n";
            return;
        }
        Policy* cur = head;
        while (cur != NULL) {
            cout << "ID: " << cur->id << " | Holder: " << cur->holder
                << " | Type: " << cur->type << " | Coverage: " << cur->coverage << "\n";
            cur = cur->next;
        }
        cout << "Total: " << count << "\n";
    }
};

// ---------- Read a number safely (no crash if the user types letters) ----------
int readInt(string message) {
    int x;
    cout << message;
    while (!(cin >> x)) {
        cin.clear();
        cin.ignore(1000, '\n');
        cout << "Invalid. Enter a number: ";
    }
    cin.ignore(1000, '\n');
    return x;
}

double readDouble(string message) {
    double x;
    cout << message;
    while (!(cin >> x)) {
        cin.clear();
        cin.ignore(1000, '\n');
        cout << "Invalid. Enter a number: ";
    }
    cin.ignore(1000, '\n');
    return x;
}

// ---------- Main menu ----------
int main() {
    PolicyList list;
    int choice;

    do {
        cout << "\n--- Policy Records ---\n";
        cout << "1. Add policy\n";
        cout << "2. Delete policy\n";
        cout << "3. Search policy\n";
        cout << "4. Display all\n";
        cout << "0. Exit\n";
        choice = readInt("Choice: ");

        if (choice == 1) {
            int id = readInt("Policy ID: ");
            string holder, type;
            cout << "Holder name: ";
            getline(cin, holder);
            cout << "Policy type (Health/Auto/Home/Life): ";
            getline(cin, type);
            double coverage = readDouble("Coverage amount: ");
            list.insert(id, holder, type, coverage);
        }
        else if (choice == 2) {
            int id = readInt("Policy ID to delete: ");
            list.remove(id);
        }
        else if (choice == 3) {
            int id = readInt("Policy ID to search: ");
            list.show(id);
        }
        else if (choice == 4) {
            list.display();
        }
        else if (choice != 0) {
            cout << "Invalid choice. Try again.\n";
        }
    } while (choice != 0);

    cout << "Goodbye!\n";
    return 0;
}