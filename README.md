# Vetual-Distruktor-
#include <iostream>
#include <string>

// Базовый класс Vehicle
class Vehicle {
protected:
    std::string brand; // Марка
    std::string model; // Модель

public:
    Vehicle(const std::string& b, const std::string& m) : brand(b), model(m) {}

    virtual ~Vehicle() {
        std::cout << "Уничтожение объекта Vehicle..." << std::endl;
    }

    virtual void display() const {
        std::cout << "Марка: " << brand << ", Модель: " << model << std::endl;
    }

    virtual void log() const {
        std::cout << "Логгирование информации о транспортном средстве..." << std::endl;
    }
};

// Производный класс Car
class Car : public Vehicle {
private:
    int doors; // Количество дверей

public:
    Car(const std::string& b, const std::string& m, int d) : Vehicle(b, m), doors(d) {}

    ~Car() override {
        std::cout << "Уничтожение объекта Car..." << std::endl;
    }

    void display() const override {
        Vehicle::display();
        std::cout << "Количество дверей: " << doors << std::endl;
    }

    void log() const override {
        Vehicle::log();
        std::cout << "Логгирование информации о машине..." << std::endl;
    }
};

// Производный класс Bike
class Bike : public Vehicle {
private:
    int gears; // Количество скоростей

public:
    Bike(const std::string& b, const std::string& m, int g) : Vehicle(b, m), gears(g) {}

    ~Bike() override {
        std::cout << "Уничтожение объекта Bike..." << std::endl;
    }

    void display() const override {
        Vehicle::display();
        std::cout << "Количество скоростей: " << gears << std::endl;
    }

    void log() const override {
        Vehicle::log();
        std::cout << "Логгирование информации о велосипеде..." << std::endl;
    }
};

int main() {
    // Динамическое выделение памяти для объектов Car и Bike
    Vehicle* vehicles[2];
    vehicles[0] = new Car("Toyota", "Corolla", 4);
    vehicles[1] = new Bike("Trek", "Mountain Bike", 21);

    // Вывод информации о транспортных средствах
    for (int i = 0; i < 2; i++) {
        vehicles[i]->display();
        vehicles[i]->log();
        std::cout << std::endl;
    }

    // Освобождение памяти
    for (int i = 0; i < 2; i++) {
        delete vehicles[i];
    }

    return 0;
}
