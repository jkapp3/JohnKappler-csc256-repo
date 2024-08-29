**I want to create a calculator program in python using the procedural paradigm. Initially, the feature will be for addition, subtraction, multiplication, and division. I will add other features such as present value, mortgage payments, etc. later so the design must easily allow this.**


To design a calculator program in Python using a procedural paradigm, you'll want to structure your code in a way that makes it easy to add future features such as present value, mortgage payments, etc. You can achieve this by breaking your code into separate functions for each feature.

Here's an initial design for your calculator with addition, subtraction, multiplication, and division operations. It’s organized so that you can easily add more features later.

Program:
python
Copy code
# Main function to run the calculator
def main():
    while True:
        print_menu()  # Display the menu options
        choice = input("Choose an operation or type 'E' to exit: ").upper()

        if choice == 'E':
            print("Exiting calculator. Goodbye!")
            break
        elif choice in ['A', 'S', 'M', 'D']:
            num1, num2 = get_numbers()
            if choice == 'A':
                result = addition(num1, num2)
                print(f"Result: {num1} + {num2} = {result}")
            elif choice == 'S':
                result = subtraction(num1, num2)
                print(f"Result: {num1} - {num2} = {result}")
            elif choice == 'M':
                result = multiplication(num1, num2)
                print(f"Result: {num1} * {num2} = {result}")
            elif choice == 'D':
                result = division(num1, num2)
                if result is not None:
                    print(f"Result: {num1} / {num2} = {result}")
        else:
            print("Invalid option, please choose a valid operation.")

# Function to print the menu options
def print_menu():
    print("\nCalculator Menu:")
    print("A: Addition")
    print("S: Subtraction")
    print("M: Multiplication")
    print("D: Division")
    print("E: Exit")

# Function to get input numbers from the user
def get_numbers():
    while True:
        try:
            num1 = float(input("Enter first number: "))
            num2 = float(input("Enter second number: "))
            return num1, num2
        except ValueError:
            print("Invalid input. Please enter numeric values.")

# Function for addition
def addition(a, b):
    return a + b

# Function for subtraction
def subtraction(a, b):
    return a - b

# Function for multiplication
def multiplication(a, b):
    return a * b

# Function for division
def division(a, b):
    if b == 0:
        print("Error: Division by zero is not allowed.")
        return None
    return a / b

# Run the calculator program
if __name__ == "__main__":
    main()
Explanation:
Procedural Structure:

Each operation (addition, subtraction, multiplication, and division) is encapsulated in its own function. This approach makes it easier to maintain and extend the code.
The main() function runs the calculator, controlling the flow of the program. It includes a loop that keeps running until the user chooses to exit.
Adding New Features:

You can add future features like present value, mortgage payments, etc., by creating new functions in a similar manner. For example, to add a function for present value, you might do something like:
python
Copy code
def present_value(future_value, rate, periods):
    return future_value / (1 + rate) ** periods
Then, update the print_menu() to include the new feature and handle the user's choice in main() just like the existing operations.

Menu-Driven Interface:

A menu-based system is used to allow the user to choose the operation they want. The design is flexible enough to easily add new options in the future by modifying the print_menu() and the corresponding logic.
Example Output:
yaml
Copy code
Calculator Menu:
A: Addition
S: Subtraction
M: Multiplication
D: Division
E: Exit
Choose an operation or type 'E' to exit: A
Enter first number: 10
Enter second number: 5
Result: 10.0 + 5.0 = 15.0

Calculator Menu:
A: Addition
S: Subtraction
M: Multiplication
D: Division
E: Exit
Choose an operation or type 'E' to exit: D
Enter first number: 10
Enter second number: 0
Error: Division by zero is not allowed.

Calculator Menu:
A: Addition
S: Subtraction
M: Multiplication
D: Division
E: Exit
Choose an operation or type 'E' to exit: E
Exiting calculator. Goodbye!
This approach allows you to keep your code organized and scalable, making it easy to add features in the future.




**Can unit tests using `Pytest` be created to test the code easily with minimum mocking?**


Yes, you can easily write unit tests using Pytest for the calculator code you provided. Since the program mostly performs simple arithmetic operations, mocking is not required for most tests. You can test the individual functions directly by passing appropriate inputs.

Here’s an example of how you might write unit tests for the calculator using Pytest:

Test File: test_calculator.py
python
Copy code
from calculator import addition, subtraction, multiplication, division  # Import the functions to test

# Test for addition function
def test_addition():
    assert addition(10, 5) == 15
    assert addition(-1, 1) == 0
    assert addition(0, 0) == 0

# Test for subtraction function
def test_subtraction():
    assert subtraction(10, 5) == 5
    assert subtraction(-1, 1) == -2
    assert subtraction(0, 0) == 0

# Test for multiplication function
def test_multiplication():
    assert multiplication(10, 5) == 50
    assert multiplication(-1, 1) == -1
    assert multiplication(0, 5) == 0

# Test for division function
def test_division():
    assert division(10, 5) == 2
    assert division(-10, 5) == -2
    assert division(0, 5) == 0
    
    # Test division by zero
    assert division(10, 0) is None  # Expecting None for division by zero
Explanation of Tests:
Addition Tests (test_addition):

We test various cases including positive numbers, a mix of positive and negative, and zero addition.
Subtraction Tests (test_subtraction):

Similar to the addition tests but for subtraction.
Multiplication Tests (test_multiplication):

Tests include standard multiplication, negative numbers, and multiplying by zero.
Division Tests (test_division):

Tests include standard division, negative numbers, and the special case of dividing by zero. The division by zero case is expected to return None, as handled in the main program.
Running the Tests:
Install pytest if you haven't already by running:

bash
Copy code
pip install pytest
Save the above test file as test_calculator.py in the same directory as your calculator.py file.

Run the tests using pytest from the command line:

bash
Copy code
pytest test_calculator.py
Output:
If everything passes, you should see output like this:

diff
Copy code
============================= test session starts ==============================
collected 4 items

test_calculator.py ....                                                   [100%]

============================== 4 passed in 0.02s ===============================
Notes:
No Mocking Required: Since the calculator functions are pure and don’t rely on external dependencies like databases or APIs, you don’t need to mock anything for these basic operations. You’re directly testing the core logic.
Extending Tests: As you add more features (e.g., present value, mortgage payments), you can simply add corresponding test cases in the same format.
This approach keeps testing straightforward and maintainable as you scale up the functionality



**Does the code meet the following principles? If not, where and how do I refactor? Code that meets SOLID principles as well as DRY, KISS, YAGNI, Law of Demeter, Composition over inheritance, Encapsulation, High Cohesion, Low Coupling, modular design, OOP principles. Code should be easy to maintain, easy to add features, and easy to test using `Pytest`.**


The provided code is procedural in nature, and you are looking to adapt it so that it adheres to several software design principles, including SOLID, DRY, KISS, YAGNI, and other principles that are more aligned with Object-Oriented Programming (OOP). To meet these principles, a refactor is required, transitioning the design from procedural to an OOP approach while maintaining ease of testing, readability, and extensibility.

Let's examine how the current code does and doesn’t meet these principles, and then refactor it.

Principles:
SOLID Principles:

Single Responsibility Principle (SRP): Each class should have only one reason to change. In the current code, there’s no clear separation of concerns.
Open/Closed Principle (OCP): Code should be open for extension but closed for modification. As new operations are added, you’d likely modify the main() function, which is against this principle.
Liskov Substitution Principle (LSP): This principle applies more to class hierarchies, which the current procedural design lacks.
Interface Segregation Principle (ISP): Not relevant here since there are no interfaces yet.
Dependency Inversion Principle (DIP): The program is dependent on procedural logic, not abstractions, which limits flexibility and extensibility.
DRY (Don't Repeat Yourself): The original code is fairly DRY, but the way operations are handled can be made more efficient by avoiding repeated conditional checks.

KISS (Keep It Simple, Stupid): The current design is simple, but as more features are added, this simplicity could be lost without proper modular design.

YAGNI (You Ain't Gonna Need It): The current implementation doesn’t over-engineer the solution, but future extensions could benefit from flexibility without adding unnecessary complexity upfront.

Law of Demeter: The current code does not violate this principle, but as we refactor into classes, we should ensure that objects only interact with their immediate collaborators.

Composition over Inheritance: Since there are no objects yet, this principle isn’t violated, but the refactor will need to avoid overusing inheritance.

Encapsulation: The current procedural design doesn’t encapsulate functionality well.

High Cohesion: There’s no modular division of functionality in the current procedural design.

Low Coupling: Adding more features would create tight coupling in the procedural design due to how the main() function handles different operations.

Refactor for SOLID, OOP, and Other Principles
We’ll refactor this into an OOP design that adheres to SOLID principles and others mentioned. Each operation will be a class, and we’ll use composition to handle different features, ensuring the code is extensible and easy to maintain.

Refactored Code (Object-Oriented Design)
python
Copy code
# calculator.py

from abc import ABC, abstractmethod

# Base class for operations (open for extension)
class Operation(ABC):
    @abstractmethod
    def execute(self, a, b):
        pass

# Concrete implementations of operations
class Addition(Operation):
    def execute(self, a, b):
        return a + b

class Subtraction(Operation):
    def execute(self, a, b):
        return a - b

class Multiplication(Operation):
    def execute(self, a, b):
        return a * b

class Division(Operation):
    def execute(self, a, b):
        if b == 0:
            raise ValueError("Division by zero is not allowed")
        return a / b

# Calculator class that uses composition to perform operations
class Calculator:
    def __init__(self):
        # Dictionary to store available operations (high cohesion)
        self.operations = {
            'A': Addition(),
            'S': Subtraction(),
            'M': Multiplication(),
            'D': Division()
        }

    def perform_operation(self, operation_code, a, b):
        operation = self.operations.get(operation_code.upper())
        if operation:
            return operation.execute(a, b)
        else:
            raise ValueError(f"Invalid operation code: {operation_code}")

# Main entry point of the program
def main():
    calculator = Calculator()

    while True:
        print_menu()
        choice = input("Choose an operation or type 'E' to exit: ").upper()

        if choice == 'E':
            print("Exiting calculator. Goodbye!")
            break
        elif choice in calculator.operations:
            num1, num2 = get_numbers()
            try:
                result = calculator.perform_operation(choice, num1, num2)
                print(f"Result: {result}")
            except ValueError as e:
                print(e)
        else:
            print("Invalid option, please choose a valid operation.")

# Helper functions
def print_menu():
    print("\nCalculator Menu:")
    print("A: Addition")
    print("S: Subtraction")
    print("M: Multiplication")
    print("D: Division")
    print("E: Exit")

def get_numbers():
    while True:
        try:
            num1 = float(input("Enter first number: "))
            num2 = float(input("Enter second number: "))
            return num1, num2
        except ValueError:
            print("Invalid input. Please enter numeric values.")

# Run the program
if __name__ == "__main__":
    main()
How the Refactor Meets the Principles:
SOLID:

SRP: Each class (Addition, Subtraction, etc.) has a single responsibility: performing its respective operation.
OCP: You can add new operations (e.g., PresentValue, MortgagePayment) without modifying the existing classes. Just add the new operation to the operations dictionary.
LSP: Each subclass of Operation can be substituted in place of its parent without affecting the program.
ISP: Each operation is focused on a single task.
DIP: The Calculator class depends on abstractions (Operation), not concrete implementations.
DRY: Repeated logic for handling operations has been removed by abstracting it into classes. The perform_operation method handles all operations uniformly.

KISS: The design is kept simple and easy to understand by following OOP principles, without introducing unnecessary complexity.

YAGNI: We haven’t introduced features that aren’t needed yet, but the design is extensible enough to add features like mortgage payments and present value.

Law of Demeter: Objects only interact with their direct dependencies. The Calculator class only interacts with the Operation objects it stores.

Composition over Inheritance: The Calculator class uses composition to manage different operations instead of inheritance, which makes the design more flexible.

Encapsulation: The Calculator class encapsulates the logic for managing operations, and the operation classes encapsulate the specific logic for each operation.

High Cohesion: Each class is highly cohesive, focusing on a single task (i.e., performing one type of operation).

Low Coupling: The classes are loosely coupled. Changes to one operation class do not affect the others.

Modular Design: The design is modular, allowing easy addition of new operations or features without touching the rest of the code.

Testing with Pytest
The OOP design makes testing even easier because each operation is encapsulated in its own class. You can create separate test cases for each class, testing their behavior independently.

Test File (test_calculator.py):
python
Copy code
import pytest
from calculator import Addition, Subtraction, Multiplication, Division

def test_addition():
    addition = Addition()
    assert addition.execute(5, 3) == 8
    assert addition.execute(-1, 1) == 0

def test_subtraction():
    subtraction = Subtraction()
    assert subtraction.execute(5, 3) == 2
    assert subtraction.execute(-1, 1) == -2

def test_multiplication():
    multiplication = Multiplication()
    assert multiplication.execute(5, 3) == 15
    assert multiplication.execute(-1, 1) == -1

def test_division():
    division = Division()
    assert division.execute(6, 3) == 2
    assert division.execute(-6, 2) == -3
    
    with pytest.raises(ValueError):
        division.execute(6, 0)
This design ensures easy maintainability, scalability, and testability. New features can be added by creating new classes, updating the menu, and adding corresponding tests without affecting existing code.


**Add a new feature that would require a database or JSON file. Modularize the code into at least four modules to help in team development, testing, maintenance, and minimizing refactoring while adding features.**



To add a new feature that requires persistent storage (such as a database or JSON file), we'll refactor the calculator into a modular design with four modules. The new feature could be saving and retrieving previous calculation results to/from a JSON file for simplicity. This feature will demonstrate how to handle persistent data while maintaining the principles of modular design, SOLID, and OOP.

We'll break the code into four main modules:

operations.py: This will handle the operations (addition, subtraction, multiplication, division).
calculator.py: This will serve as the core module, managing the calculator logic and interaction with operations.
storage.py: This module will handle reading/writing data to/from a JSON file (persistence).
main.py: The entry point of the program that brings everything together.
1. operations.py (Handles all operations)
python
Copy code
# operations.py

from abc import ABC, abstractmethod

class Operation(ABC):
    @abstractmethod
    def execute(self, a, b):
        pass

class Addition(Operation):
    def execute(self, a, b):
        return a + b

class Subtraction(Operation):
    def execute(self, a, b):
        return a - b

class Multiplication(Operation):
    def execute(self, a, b):
        return a * b

class Division(Operation):
    def execute(self, a, b):
        if b == 0:
            raise ValueError("Division by zero is not allowed")
        return a / b
2. calculator.py (Calculator logic, using the operations)
python
Copy code
# calculator.py

from operations import Addition, Subtraction, Multiplication, Division

class Calculator:
    def __init__(self):
        # High cohesion: operations are handled in one place
        self.operations = {
            'A': Addition(),
            'S': Subtraction(),
            'M': Multiplication(),
            'D': Division()
        }

    def perform_operation(self, operation_code, a, b):
        operation = self.operations.get(operation_code.upper())
        if operation:
            return operation.execute(a, b)
        else:
            raise ValueError(f"Invalid operation code: {operation_code}")

    def available_operations(self):
        return self.operations.keys()
3. storage.py (Handles reading and writing from a JSON file)
python
Copy code
# storage.py

import json
import os

class StorageManager:
    def __init__(self, filename='calculations.json'):
        self.filename = filename

    def save_result(self, operation, num1, num2, result):
        data = {
            "operation": operation,
            "num1": num1,
            "num2": num2,
            "result": result
        }

        if not os.path.exists(self.filename):
            with open(self.filename, 'w') as file:
                json.dump([], file)

        with open(self.filename, 'r+') as file:
            current_data = json.load(file)
            current_data.append(data)
            file.seek(0)
            json.dump(current_data, file, indent=4)

    def retrieve_results(self):
        if os.path.exists(self.filename):
            with open(self.filename, 'r') as file:
                return json.load(file)
        return []

    def clear_results(self):
        if os.path.exists(self.filename):
            with open(self.filename, 'w') as file:
                json.dump([], file)
4. main.py (Entry point that brings everything together)
python
Copy code
# main.py

from calculator import Calculator
from storage import StorageManager

def main():
    calculator = Calculator()
    storage = StorageManager()

    while True:
        print_menu()
        choice = input("Choose an operation (or type 'E' to exit, 'R' to retrieve saved results): ").upper()

        if choice == 'E':
            print("Exiting calculator. Goodbye!")
            break
        elif choice == 'R':
            print_saved_results(storage)
        elif choice in calculator.available_operations():
            num1, num2 = get_numbers()
            try:
                result = calculator.perform_operation(choice, num1, num2)
                print(f"Result: {result}")
                # Save result to JSON
                storage.save_result(choice, num1, num2, result)
            except ValueError as e:
                print(e)
        else:
            print("Invalid option, please choose a valid operation.")

def print_menu():
    print("\nCalculator Menu:")
    print("A: Addition")
    print("S: Subtraction")
    print("M: Multiplication")
    print("D: Division")
    print("R: Retrieve previous results")
    print("E: Exit")

def get_numbers():
    while True:
        try:
            num1 = float(input("Enter first number: "))
            num2 = float(input("Enter second number: "))
            return num1, num2
        except ValueError:
            print("Invalid input. Please enter numeric values.")

def print_saved_results(storage):
    results = storage.retrieve_results()
    if results:
        print("\nSaved Results:")
        for result in results:
            print(f"{result['num1']} {result['operation']} {result['num2']} = {result['result']}")
    else:
        print("No saved results found.")

if __name__ == "__main__":
    main()
Breakdown of the Modules:
operations.py: This module defines the operations (Addition, Subtraction, Multiplication, Division) with a base abstract class Operation. Each class implements its own execute() method. This is in line with High Cohesion and Single Responsibility Principle (SRP).

calculator.py: This is the core of the calculator, managing the available operations and performing them when requested. It decouples the operations from the rest of the logic, adhering to Low Coupling and Open/Closed Principle (OCP) as new operations can be added without modifying existing ones.

storage.py: This module manages saving and retrieving calculation results using a JSON file. It ensures that the persistence logic is encapsulated and separated from the core calculator logic, which promotes Low Coupling and Single Responsibility Principle (SRP).

main.py: The entry point that ties everything together. It includes the menu system and user interaction logic. Since the calculator and storage are encapsulated in their own modules, main.py focuses only on controlling the flow of the program, promoting High Cohesion.

Adding New Features
This design is highly modular and extensible. Adding a new feature, such as another operation or a new type of persistent storage, will require minimal changes:

New Operation: Just add a new class (e.g., PresentValue) in operations.py and register it in calculator.py.

New Storage Backend: You could add a new storage class (e.g., using a database like SQLite) in storage.py and switch between storage backends by configuring StorageManager.

Testing with Pytest
Testing becomes more straightforward due to the modular design. You can write unit tests for each module separately without much mocking.

Example Unit Test (test_operations.py):
python
Copy code
# test_operations.py
from operations import Addition, Subtraction, Multiplication, Division
import pytest

def test_addition():
    addition = Addition()
    assert addition.execute(5, 3) == 8

def test_subtraction():
    subtraction = Subtraction()
    assert subtraction.execute(5, 3) == 2

def test_multiplication():
    multiplication = Multiplication()
    assert multiplication.execute(5, 3) == 15

def test_division():
    division = Division()
    assert division.execute(6, 3) == 2
    with pytest.raises(ValueError):
        division.execute(6, 0)
Example Unit Test (test_storage.py):
python
Copy code
# test_storage.py
import os
from storage import StorageManager

def test_save_and_retrieve_results():
    storage = StorageManager("test_calculations.json")
    storage.clear_results()  # Start fresh
    storage.save_result('A', 5, 3, 8)
    
    results = storage.retrieve_results()
    assert len(results) == 1
    assert results[0]['operation'] == 'A'
    assert results[0]['num1'] == 5
    assert results[0]['num2'] == 3
    assert results[0]['result'] == 8
    
    # Clean up test file
    os.remove("test_calculations.json")
Conclusion
This refactor breaks the program into four clear, modular components:

Operations: Handles all math operations.
Calculator: Manages the business logic of performing calculations.
Storage: Manages saving and retrieving results to/from a JSON file.
Main: The entry point that handles user interaction.
This design adheres to SOLID, DRY, and other best practices while ensuring ease of testing, team development, and feature expansion.


**If I wanted to eventually turn this into a web application, what refactoring should I do to allow this in the future?**

To refactor the current modular codebase with future scalability in mind (e.g., turning it into a web application), we should focus on making the architecture more flexible, decoupled, and layered to support different interfaces, such as a web UI. This will require focusing on separation of concerns, abstracting dependencies, and ensuring that the business logic (calculations and persistence) can be reused without modification.

Here’s a step-by-step breakdown of how to refactor the current design in anticipation of transforming it into a web application:

Refactoring Goals:
Separation of Concerns (SoC): Separate business logic (calculations) from the presentation logic (web or CLI). This ensures that the same business logic can be reused across different interfaces.
Service Layer: Introduce a service layer to manage interactions between different components, like the calculator and storage.
Dependency Injection: Introduce dependency injection to manage the dependencies of components like storage backends and the calculator logic, making it easier to swap out implementations (e.g., use a database instead of JSON).
REST API-ready: Prepare the logic to be exposed via a web API (e.g., using Flask or FastAPI) so that the web interface can interact with the backend easily.
Statelessness: Ensure stateless business logic to facilitate the transition to a web service that handles HTTP requests.
Validation Layer: Add proper input validation and error handling in preparation for handling user input from web forms.
Persistence Layer: Decouple the storage management from the rest of the code so that you can later use databases, cloud storage, etc., without major changes.
Step-by-Step Refactor
Introduce a Service Layer: This layer acts as an intermediary between the business logic (calculator) and the storage logic, allowing you to reuse the same business logic across different interfaces (e.g., CLI, web, API).

Decouple Storage: Make storage interchangeable (i.e., use JSON, databases, or other forms of storage without refactoring the whole system).

Introduce Dependency Injection: Pass the calculator and storage dependencies into the service layer, allowing different modules to easily swap in other services (e.g., from JSON to SQL storage).

Prepare for Web Framework: Prepare the application so that it can easily plug into a web framework like Flask or FastAPI.

Refactored Design:
1. operations.py (No changes, remains the same)
python
Copy code
# operations.py

from abc import ABC, abstractmethod

class Operation(ABC):
    @abstractmethod
    def execute(self, a, b):
        pass

class Addition(Operation):
    def execute(self, a, b):
        return a + b

class Subtraction(Operation):
    def execute(self, a, b):
        return a - b

class Multiplication(Operation):
    def execute(self, a, b):
        return a * b

class Division(Operation):
    def execute(self, a, b):
        if b == 0:
            raise ValueError("Division by zero is not allowed")
        return a / b
2. calculator.py (Decouple logic, stateless)
python
Copy code
# calculator.py

from operations import Addition, Subtraction, Multiplication, Division

class Calculator:
    def __init__(self):
        self.operations = {
            'A': Addition(),
            'S': Subtraction(),
            'M': Multiplication(),
            'D': Division()
        }

    def perform_operation(self, operation_code, a, b):
        operation = self.operations.get(operation_code.upper())
        if operation:
            return operation.execute(a, b)
        else:
            raise ValueError(f"Invalid operation code: {operation_code}")

    def available_operations(self):
        return self.operations.keys()
3. storage.py (Decouple the storage, use Dependency Injection)
python
Copy code
# storage.py

import json
import os

class StorageInterface:
    def save_result(self, operation, num1, num2, result):
        pass

    def retrieve_results(self):
        pass

    def clear_results(self):
        pass

class JSONStorage(StorageInterface):
    def __init__(self, filename='calculations.json'):
        self.filename = filename

    def save_result(self, operation, num1, num2, result):
        data = {
            "operation": operation,
            "num1": num1,
            "num2": num2,
            "result": result
        }

        if not os.path.exists(self.filename):
            with open(self.filename, 'w') as file:
                json.dump([], file)

        with open(self.filename, 'r+') as file:
            current_data = json.load(file)
            current_data.append(data)
            file.seek(0)
            json.dump(current_data, file, indent=4)

    def retrieve_results(self):
        if os.path.exists(self.filename):
            with open(self.filename, 'r') as file:
                return json.load(file)
        return []

    def clear_results(self):
        if os.path.exists(self.filename):
            with open(self.filename, 'w') as file:
                json.dump([], file)
This module can now easily be swapped for another storage system, such as a database (e.g., SQLAlchemy for SQL).

4. service.py (Service Layer that handles business logic and storage interaction)
python
Copy code
# service.py

from calculator import Calculator
from storage import StorageInterface

class CalculatorService:
    def __init__(self, storage: StorageInterface):
        self.calculator = Calculator()
        self.storage = storage

    def calculate_and_save(self, operation_code, num1, num2):
        result = self.calculator.perform_operation(operation_code, num1, num2)
        self.storage.save_result(operation_code, num1, num2, result)
        return result

    def get_saved_results(self):
        return self.storage.retrieve_results()

    def clear_results(self):
        self.storage.clear_results()
5. main.py (CLI interface remains, but can be swapped for a web app)
python
Copy code
# main.py

from service import CalculatorService
from storage import JSONStorage

def main():
    storage = JSONStorage()  # This can be swapped with a DB later
    calculator_service = CalculatorService(storage)

    while True:
        print_menu()
        choice = input("Choose an operation (or type 'E' to exit, 'R' to retrieve saved results): ").upper()

        if choice == 'E':
            print("Exiting calculator. Goodbye!")
            break
        elif choice == 'R':
            print_saved_results(calculator_service)
        elif choice in calculator_service.calculator.available_operations():
            num1, num2 = get_numbers()
            try:
                result = calculator_service.calculate_and_save(choice, num1, num2)
                print(f"Result: {result}")
            except ValueError as e:
                print(e)
        else:
            print("Invalid option, please choose a valid operation.")

def print_menu():
    print("\nCalculator Menu:")
    print("A: Addition")
    print("S: Subtraction")
    print("M: Multiplication")
    print("D: Division")
    print("R: Retrieve previous results")
    print("E: Exit")

def get_numbers():
    while True:
        try:
            num1 = float(input("Enter first number: "))
            num2 = float(input("Enter second number: "))
            return num1, num2
        except ValueError:
            print("Invalid input. Please enter numeric values.")

def print_saved_results(service):
    results = service.get_saved_results()
    if results:
        print("\nSaved Results:")
        for result in results:
            print(f"{result['num1']} {result['operation']} {result['num2']} = {result['result']}")
    else:
        print("No saved results found.")

if __name__ == "__main__":
    main()
Preparing for Web Application Development
Web Framework: To convert this into a web application, you could use a web framework like Flask or FastAPI.

You will create HTTP endpoints that map to the CalculatorService for operations and storage interactions.
Flask Example:

Create a web.py file that sets up the web interface.

python
Copy code
# web.py
from flask import Flask, request, jsonify
from service import CalculatorService
from storage import JSONStorage

app = Flask(__name__)
storage = JSONStorage()
service = CalculatorService(storage)

@app.route("/calculate", methods=["POST"])
def calculate():
    data = request.json
    operation = data.get("operation")
    num1 = float(data.get("num1"))
    num2 = float(data.get("num2"))
    
    try:
        result = service.calculate_and_save(operation, num1, num2)
        return jsonify({"result": result}), 200
    except ValueError as e:
        return jsonify({"error": str(e)}), 400

@app.route("/results", methods=["GET"])
def get_results():
    results = service.get_saved_results()
    return jsonify(results), 200

if __name__ == "__main__":
    app.run(debug=True)
Front-end: You can later add a web interface using HTML/JavaScript, connecting to the Flask API endpoints for performing calculations and retrieving results.

Database: Swap JSONStorage with a real database like SQLite, PostgreSQL, or MySQL using ORM libraries like SQLAlchemy. The service layer and core logic won’t need major changes, thanks to decoupling.

Refactor Summary:
Separation of Concerns: The business logic (calculations) is now decoupled from storage, making it easier to swap components (e.g., databases, APIs).
Service Layer: Centralizes the business logic and integrates with storage in a cohesive way.
REST API-ready: The code is ready to be integrated with a web framework like Flask or FastAPI for web development.
Flexible Architecture: Adding new features (like another storage backend or advanced calculations) will be easier without modifying existing logic.
This refactor ensures the codebase remains modular, extensible, and scalable as you move toward a web application while still following best practices like SOLID, DRY, and KISS.
