# OOP Characteristic
Karakteristik OOP terbagi menjadi 3 yaitu : 
- Abstraction
- Encapsulation
- Inheritance
- Polymorphism

# Abstraction
Proses penjelasan kegunaan tanpa memberi tahu bagaimana cara kerjanya, di implementasikan dalam proses instantiate
```js

class Car {
    constructor(brand, engineCapacity, price) {
        this.brand = brand
        this.engineCapacity = engineCapacity
        this.price = price
    }

    start() {
        console.log("Starting car...");
    }

    brake() {
        console.log("Slowing down...");
    }

    stop() {
        console.log("Stopping the car");
    }

    regulation() {
        if (this.engineCapacity <= 1200) {
            return "LCGC"
        } else {
            return "Not LCGC"
        }
    }
}

const myCar = new Car("Mazda", 1500, 15000000)
console.log(myCar);
myCar.start()
myCar.brake()
myCar.stop()
```

# Encapsulation
Menyembunyikan detail-detail penting atau internal yang tidak perlu ditampilkan keluar, diimplementasikan dalam pembuatan private property
```js
class Motorcycle {
    brand
    #price // cuman bisa diakses di classnya sendiri
    constructor(brand, engineCapacity, price) {
        this.brand = brand // public property
        this.engineCapacity = engineCapacity
        this.#price = price // private property
    }

    showPrice() { // beda getter dan instance method adalah pemanggilannya, instance method harus di invoke
        return this.#price
    }

    get price() { // untuk mendapatkan private properti
        return this.#price
    }

    set changePrice(newPrice) { // untuk mengubah value private properti
        this.#price = newPrice
    }

    start() {
        console.log("Starting motorcycle...");
    }

    brake() {
        console.log("Slowing down...");
    }

    stop() {
        console.log("Stopping the motorcycle");
    }
}

const myMotorcycle = new Motorcycle("Honda", 250, 5000000)
myMotorcycle.changePrice = 90000000
myMotorcycle.newBrand = "Nissan"
console.log(myMotorcycle.newBrand);
```

# Inheritance
Proses pewarisan properti / karakteristik dari parent ke anaknya, diimplementasikan dengan membuat custom subclass menggunakan `extends`

Untuk mengakses properti / method parent, gunakan `super` keyword
```js
class Nissan extends Car {
    constructor(cc, harga, color) {
        super("Nissan", cc, harga) // fokus ke constructor parent
        this.color = color
    }

    super.start() // fokus ke method parent, hanya contoh pemanggilan method aja, ga berguna disini
}

const myNissan = new Nissan(1200, 500000000, "blue")
console.log(myNissan);
```

# Polymorphism
Proses `overriding` / `penumpukan` method yang sudah ada di parent class, sehingga bisa mengubah perilaku method tersebut di subclass
```js
class Nissan extends Car {
    constructor(cc, harga, color) {
        super("Nissan", cc, harga)
        this.color = color
    }

    brake() { // Polymorphism = overriding/numpuk suatu method yang udah ada di parent
        super.brake()
        console.log("Drifting bro like han tokyo drift...");
    }

    regulation() { // Polymorphism
        if (this.engineCapacity <= 1200) {
            if (this.color == "red") {
                return "LCGC"
            } else {
                return "Not matching color"
            }
        } else {
            return "Not LCGC"
        }
    }
}

const myNissan = new Nissan(1200, 500000000, "blue")
console.log(myNissan);

myNissan.brake()
```
