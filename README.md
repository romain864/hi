product.h

#pragma once
#include <string>

class Product {
private:
    std::string name;
    double price;

public:
    Product(std::string name, double price);
    std::string getName();
    double getPrice();
};






product.cpp

#include "Product.h"

// Constructeur
Product::Product(std::string name, double price)
    : name(name), price(price) {
}

std::string Product::getName() {
    return name;
}





cart.h

#pragma once
#include <vector>
#include "Product.h"

class Cart {
private:
    std::vector<Product> products;

public:
    void addProduct(Product product);
    std::vector<Product> getProducts();
    double getTotalPrice();
    void printCart();
};





cart.cpp

#include "Cart.h"
#include <iostream>

void Cart::addProduct(Product product) {
    products.push_back(product);
}

std::vector<Product> Cart::getProducts() {
    return products;
}

double Cart::getTotalPrice() {
    double total = 0.0;
    for (int i = 0; i < products.size(); i++) {
        total += products[i].getPrice();
    }
    return total;
}

void Cart::printCart() {
    std::cout << "=== CONTENU DU PANIER ===" << std::endl;

    if (products.empty()) {
        std::cout << "Le panier est vide." << std::endl;
        return;
    }

    for (int i = 0; i < products.size(); i++) {
        std::cout << i + 1 << ". " << products[i].getName() 
                  << " : " << products[i].getPrice() << " euros" << std::endl;
    }

    std::cout << "--------------------------" << std::endl;
    std::cout << "TOTAL : " << getTotalPrice() << " euros" << std::endl;
}




main.cpp

#include <iostream>
#include "Product.h"
#include "Cart.h"

int main() {
    // 1. Création du panier
    Cart monPanier;

    // 2. Création de produits
    Product p1("Pommes", 2.50);
    Product p2("Ordinateur Gaming", 1299.00);
    Product p3("Clavier Mecanique", 85.50);

    // 3. Ajout au panier
    monPanier.addProduct(p1);
    monPanier.addProduct(p2);
    monPanier.addProduct(p3);

    // 4. Affichage (C'est cette ligne qui appelait l'erreur)
    monPanier.printCart();

    return 0;
}

double Product::getPrice() {
    return price;
}
