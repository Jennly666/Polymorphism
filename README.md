#include <iostream>
#include <vector>

class Pizza {
public:
    virtual ~Pizza() {}

    virtual void printDetails() const = 0;
    virtual int calculatePrice() const = 0;
    virtual void setSize(int size) = 0;
    virtual void addSalt(int amount) = 0;
    virtual void addCheese(int amount) = 0;
};

class Napoletana : public Pizza {
private:
    std::string name;
    std::string description;
    int size;
    int salt;
    int cheese;

public:
    Napoletana() : name("Napoletana"), description("Tomato sauce, mozzarella, oregano, anchovies"), size(25), salt(0), cheese(0) {}

    void printDetails() const override {
        std::cout << "Name: " << name << std::endl;
        std::cout << "Description: " << description << std::endl;
        std::cout << "Size: " << size << std::endl;
        std::cout << "Cheese: " << cheese << std::endl;
        std::cout << "Salt: " << salt << std::endl;
        std::cout << "Price: " << calculatePrice() << std::endl;
    }

    int calculatePrice() const override {
        return size * 10 + cheese * 5 + salt * 2;
    }

    void setSize(int newSize) override {
        size = newSize;
    }

    void addSalt(int amount) override {
        salt += amount;
    }

    void addCheese(int amount) override {
        cheese += amount;
    }
};

class Margherita : public Pizza {
private:
    std::string name;
    std::string description;
    int size;
    int salt;
    int cheese;

public:
    Margherita() : name("Margherita"), description("Tomato sauce, mozzarella, oregano."), size(25), salt(0), cheese(0) {}

    void printDetails() const override {
        std::cout << "Name: " << name << std::endl;
        std::cout << "Description: " << description << std::endl;
        std::cout << "Size: " << size << std::endl;
        std::cout << "Cheese: " << cheese << std::endl;
        std::cout << "Salt: " << salt << std::endl;
        std::cout << "Price: " << calculatePrice() << std::endl;
    }

    int calculatePrice() const override {
        return size * 8 + cheese * 4 + salt * 2;
    }

    void setSize(int newSize) override {
        size = newSize;
    }

    void addSalt(int amount) override {
        salt += amount;
    }

    void addCheese(int amount) override {
        cheese += amount;
    }
};

class Carbonara : public Pizza {
private:
    std::string name;
    std::string description;
    int size;
    int salt;
    int cheese;

public:
    Carbonara() : name("Carbonara"), description("Cream sauce, mozzarella, bacon, eggs, parmesan, black pepper."), size(25), salt(0), cheese(0) {}

    void printDetails() const override {
        std::cout << "Name: " << name << std::endl;
        std::cout << "Description: " << description << std::endl;
        std::cout << "Size: " << size << std::endl;
        std::cout << "Cheese: " << cheese << std::endl;
        std::cout << "Salt: " << salt << std::endl;
        std::cout << "Price: " << calculatePrice() << std::endl;
    }

    int calculatePrice() const override {
        return size * 12 + cheese * 6 + salt * 3;
    }

    void setSize(int newSize) override {
        size = newSize;
    }

    void addSalt(int amount) override {
        salt += amount;
    }

    void addCheese(int amount) override {
        cheese += amount;
    }
};

class Marinara : public Pizza {
private:
    std::string name;
    std::string description;
    int size;
    int salt;
    int cheese;

public:
    Marinara() : name("Marinara"), description("Tomato sauce, garlic, oregano, basil."), size(25), salt(0), cheese(0) {}

    void printDetails() const override {
        std::cout << "Name: " << name << std::endl;
        std::cout << "Description: " << description << std::endl;
        std::cout << "Size: " << size << std::endl;
        std::cout << "Cheese: " << cheese << std::endl;
        std::cout << "Salt: " << salt << std::endl;
        std::cout << "Price: " << calculatePrice() << std::endl;
    }

    int calculatePrice() const override {
        return size * 9 + cheese * 4 + salt * 2;
    }

    void setSize(int newSize) override {
        size = newSize;
    }

    void addSalt(int amount) override {
        salt += amount;
    }

    void addCheese(int amount) override {
        cheese += amount;
    }
};

class PizzaOrder {
private:
    std::vector<Pizza*> pizzas;

public:
    ~PizzaOrder() {
        clearOrder();
    }

    void addPizza(Pizza* pizza) {
        pizzas.push_back(pizza);
    }

    void printOrder() const {
        std::cout << "YOUR ORDER:" << std::endl;
        std::cout << "----------------------------------------" << std::endl;

        int total = 0;
        for (const auto& pizza : pizzas) {
            std::cout << "position" << std::endl;
            pizza->printDetails();
            std::cout << "----------------------------------------" << std::endl;
            total += pizza->calculatePrice();
        }

        std::cout << "TOTAL: " << total << std::endl;
    }

    void clearOrder() {
        for (auto pizza : pizzas) {
            delete pizza;
        }
        pizzas.clear();
    }
};

int main() {
    PizzaOrder order;

    int choice;
    do {
        std::cout << "1) Napoletana\n2) Margherita\n3) Carbonara\n4) Marinara\nEnter 1-4 to select pizza or 0 to finish: ";
        std::cin >> choice;

        if (choice >= 1 && choice <= 4) {
            Pizza* pizza = nullptr;
            switch (choice) {
            case 1:
                pizza = new Napoletana();
                break;
            case 2:
                pizza = new Margherita();
                break;
            case 3:
                pizza = new Carbonara();
                break;
            case 4:
                pizza = new Marinara();
                break;
            }

            if (pizza) {
                int sizeChoice;
                std::cout << "1) 25\n2) 30\n3) 35\n4) 40\nEnter 1-4 to choose pizza size: ";
                std::cin >> sizeChoice;
                pizza->setSize(20 + sizeChoice * 5);

                int saltAmount, cheeseAmount;
                std::cout << "Choose salt (0-10): ";
                std::cin >> saltAmount;
                pizza->addSalt(saltAmount);

                std::cout << "Choose cheese (0-10): ";
                std::cin >> cheeseAmount;
                pizza->addCheese(cheeseAmount);

                order.addPizza(pizza);
            }
        }
        else if (choice == 0) {
            order.printOrder();
            order.clearOrder();
        }
    } while (choice != 0);

    return 0;
}
