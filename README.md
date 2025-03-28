# Vetual-Distruktor-
#include <iostream>
#include <string>

// Базовый класс Vehicle
class Vehicle {
protected:
    static int idCounter; // Статический счетчик ID
    int id; // ID для каждой фигуры
    std::string brand; // Марка транспортного средства
    std::string model; // Модель транспортного средства

public:
    Vehicle(const std::string &b, const std::string &m) : brand(b), model(m) {
        id = ++idCounter; // Генерация уникального ID
    }

    virtual ~Vehicle() {
        std::cout << "Уничтожение объекта Vehicle..." << std::endl;
    }

    virtual void display() const {
        std::cout << "Brand: " << brand << ", Model: " << model << ", ID: " << id << std::endl;
    }
};

// Инициализация статического члена idCounter
int Vehicle::idCounter = 0;

// Класс Car, наследующий от Vehicle
class Car : public Vehicle {
private:
    int doors; // Количество дверей

public:
    Car(const std::string &b, const std::string &m, int d) : Vehicle(b, m), doors(d) {}

    ~Car() override {
        std::cout << "Уничтожение объекта Car..." << std::endl;
    }

    void display() const override {
        std::cout << "Car ID: " << getId() 
                  << ", Brand: " << brand 
                  << ", Model: " << model 
                  << ", Doors: " << doors << std::endl;
    }
};

// Класс Bike, наследующий от Vehicle
class Bike : public Vehicle {
private:
    int gears; // Количество скоростей

public:
    Bike(const std::string &b, const std::string &m, int g) : Vehicle(b, m), gears(g) {}

    ~Bike() override {
        std::cout << "Уничтожение объекта Bike..." << std::endl;
    }

    void display() const override {
        std::cout << "Bike ID: " << getId() 
                  << ", Brand: " << brand 
                  << ", Model: " << model 
                  << ", Gears: " << gears << std::endl;
    }
};

// Инициализация вызова
int main() {
    // Создаем массив указателей на vehicles
    Vehicle *vehicles[2];

    // Динамически создаем объекты Car и Bike
    vehicles[0] = new Car("Toyota", "Corolla", 4);
    vehicles[1] = new Bike("Yamaha", "YZF-R1", 6);

    // Вывод информации о каждом транспортном средстве
    for (int i = 0; i < 2; ++i) {
        vehicles[i]->display();
    }

    // Освобождение памяти
    for (int i = 0; i < 2; ++i) {
        delete vehicles[i]; // Удаляем динамически выделенные объекты
    }

    return 0;
}
