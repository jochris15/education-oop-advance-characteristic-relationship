# OOP Characteristic
Karakteristik OOP terbagi menjadi 3 yaitu : 
- Abstraction
- Encapsulation
- Inheritance

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
Proses pewarisan properti / karakteristik dari parent ke anaknya, diimplementasikan dengan membuat custom subclass menggunakan ``extends``
```js
class Nissan extends Car {
    constructor(cc, harga, color) {
        super("Nissan", cc, harga) // fokus ke constructor parent
        this.color = color
    }

    brake() { // Polymorphism = overriding/numpuk suatu method yang udah ada di parent
        super.brake()
        console.log("Drifting bro like han tokyo drift...");
    }

    regulation() {
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

# Object Relationship
## Composition
- Hubungan antar class yang saling ketergantungan
- Sub class di instantiate di main class, kalau main class di delete, sub class tidak berguna
<br>

```js
class Smartphone {
    static notif = 'Hello World'
    // ini variable statis milik class
    constructor(brand, camera, memory, batteryPercentage) {
        this.brand = brand
        this.camera = camera
        this.memory = memory
        this.battery = new Battery(batteryPercentage)
        this.application = []
    }
}

class Battery {
    constructor(batteryPercentage) {
        this.batteryPercentage = batteryPercentage
    }
}

class Application {
    constructor(name, category) {
        this.name = name
        this.category = category
    }
}

const ipon = new Smartphone('Apple', '100mp', 256, 90)
ipon.installApp('Instagram', 'Sosmed')
ipon.installApp('Mobile Legend', 'MOBA')
console.log(ipon);
```

## Aggregation
- Hubungan antar class yang independent
- Bisa berdiri sendiri, instantiate kedua classnya masing-masing diluar 
- Jika main class di delete , subclass tetep bisa berdiri sendiri
<br>

```js
class Person {
    constructor(name, gender, phone = []) {
        this.name = name
        this.gender = gender
        this.phone = phone
    }
}

const samsul = new Smartphone('Android', '100mp', 256, 100)
const jeff = new Person('jeff', 'pria', samsul)
console.log(jeff.phone);
```

# Method
## Instance Method
- Sebuah method yang dimiliki oleh object instance
- Jadi jika mau dipake, harus melakukan proses instantiate dulu
- Bisa akses properti dari object instance itu sendiri
## Static Method
- Sebuah method yang dimiliki oleh classnya tersebut, bukan object instance
- Jadi bisa dipake tanpa harus melakukan proses instantiate
- Tidak bisa akses properti object instance, tapi bisa akses properti statis dari class
<br>
<br>

```js
class Smartphone {
    static notif = 'Hello World'
    // ini variable statis milik class
    constructor(brand, camera, memory, batteryPercentage) {
        this.brand = brand
        this.camera = camera
        this.memory = memory
        this.battery = new Battery(batteryPercentage)
        this.application = []
    }

    installApp(name, category) {
        let app = new Application(name, category)
        this.application.push(app)
    } // instance method, punya object instance, kalo mau pake harus instantiate dulu

    static notification() {
        console.log(this.notif + 'new notification');
    } // static method, punya classnya, bisa langsung dipake tanpa proses instantiate
}
```
