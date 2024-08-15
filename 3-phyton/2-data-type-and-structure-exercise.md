## **Data Types and Structures**

**Objective:**
- Implement a Python program that utilizes lists, tuples, dictionaries, and sets to manage a simple contact list.

**Exercise:**
1. **Create a contact list** (using a list of dictionaries):
   - Each contact should have a name (string), phone number (string), and email (string).
   - Example:
     ```python
     contacts = [
         {"name": "Alice", "phone": "123-456-7890", "email": "alice@example.com"},
         {"name": "Bob", "phone": "987-654-3210", "email": "bob@example.com"}
     ]
     ```

2. **Implement the following features:**
   - **Add a new contact**: Prompt the user to enter a name, phone number, and email, and add this contact to the list.
   - **Remove a contact by name**: Prompt the user for a name, find the contact, and remove it.
   - **Search for a contact by name**: Prompt the user for a name, find and display the contact's details.
   - **Display all contacts**: Show all contacts in the list.

**Example Implementation:**
```python
def add_contact(contacts):
    name = input("Enter contact name: ")
    phone = input("Enter phone number: ")
    email = input("Enter email: ")
    contacts.append({"name": name, "phone": phone, "email": email})
    print(f"Contact {name} added.")

def remove_contact(contacts):
    name = input("Enter the name of the contact to remove: ")
    for contact in contacts:
        if contact["name"].lower() == name.lower():
            contacts.remove(contact)
            print(f"Contact {name} removed.")
            return
    print("Contact not found.")

def