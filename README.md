//zadanie 1
const currentUser = {
  name: "Jan",
  surname: "Kowalski",
  email: "jan.kowalski@example.com",
  www: "https://jan.dev",
  userType: "admin",
  isActive: true,

  show() {
    console.log(`Imię: ${this.name}`);
    console.log(`Nazwisko: ${this.surname}`);
    console.log(`Email: ${this.email}`);
    console.log(`WWW: ${this.www}`);
    console.log(`Typ użytkownika: ${this.userType}`);
    console.log(`Aktywny: ${this.isActive}`);
  },

  setActive(active) {
    this.isActive = active;
  }
};

// Пример использования
currentUser.show();          // Показываем пользователя
currentUser.setActive(false); // Деактивируем
currentUser.show();          // Снова показываем


//zadanie 2
class Book {
  constructor() {
    this.users = [];
  }

  addUser(name, age, phone) {
    this.users.push({ name, age, phone });
  }

  showUsers() {
    console.log("Wszyscy użytkownicy w książce:");
    this.users.forEach((user, index) => {
      console.log(`${index + 1}. ${user.name}, ${user.age} lat, tel: ${user.phone}`);
    });
  }

  findByName(name) {
    const found = this.users.find(user => user.name === name);
    console.log(found || false);
  }

  findByPhone(phone) {
    const found = this.users.find(user => user.phone === phone);
    console.log(found || false);
  }

  getCount() {
    console.log(`Liczba użytkowników: ${this.users.length}`);
  }
}

// Пример использования
const myBook = new Book();
myBook.addUser("Anna", 28, "123456789");
myBook.addUser("Jan", 32, "987654321");
myBook.showUsers();
myBook.findByName("Anna");
myBook.findByPhone("000000000");
myBook.getCount();


//zadanie 3
const text = {
  check(txt, word) {
    return txt.includes(word);
  },

  getCount(txt) {
    return txt.length;
  },

  getWordsCount(txt) {
    return txt.trim().split(/\s+/).length;
  },

  setCapitalize(txt) {
    return txt
      .split(" ")
      .map(word => word.charAt(0).toUpperCase() + word.slice(1))
      .join(" ");
  },

  setMix(txt) {
    return txt
      .split("")
      .map((char, index) =>
        index % 2 === 0 ? char.toLowerCase() : char.toUpperCase()
      )
      .join("");
  },

  generateRandom(lng) {
    const letters = "abcdefghijklmnopqrstuvwxyz";
    let result = "";
    for (let i = 0; i < lng; i++) {
      const rand = Math.floor(Math.random() * letters.length);
      result += letters[rand];
    }
    return result;
  }
};

// Примеры:
console.log(text.check("ala ma kota", "kota")); // true
console.log(text.getCount("ala ma kota"));      // 11
console.log(text.getWordsCount("Ala ma kota")); // 3
console.log(text.setCapitalize("ala ma kota")); // "Ala Ma Kota"
console.log(text.setMix("ala ma kota"));        // "aLa mA KoTa"
console.log(text.generateRandom(10));           // напр., "kjsudfjwei"



//zadanie 4
String.prototype.mirror = function () {
  return this.split("").reverse().join("");
};

// Пример использования:
console.log("Ala ma kota".mirror()); // "atok am alA"


//zadanie 5
a) 
function outer() {
  let count = 0;
  return function inner() {
    count++;
    return count;
  }
}

const counter = outer();
counter(); // 1
counter(); // 2

b)
function createCounter() {
  let count = 0;

  return function () {
    count++;
    return count;
  }
}

// Пример использования:
const counter1 = createCounter();
console.log(counter1()); // 1
console.log(counter1()); // 2
console.log(counter1()); // 3

const counter2 = createCounter();
console.log(counter2()); // 1 (независимый счётчик)
console.log(counter2()); // 2



//zadanie
// Базовый класс
class Product {
  constructor(name, price) {
    this.name = name;
    this.price = price;
  }
}

// Наследник с количеством
class CartProduct extends Product {
  constructor(name, price, quantity) {
    super(name, price);
    this.quantity = quantity;
  }

  getTotal() {
    return this.price * this.quantity;
  }
}

// Пример использования
const cart = [
  new CartProduct("Jabłko", 2, 5),
  new CartProduct("Chleb", 4, 2),
  new CartProduct("Mleko", 3, 1),
];

function getCartSum(cart) {
  return cart.reduce((sum, item) => sum + item.getTotal(), 0);
}

console.log("Suma koszyka:", getCartSum(cart)); // => Suma koszyka: 21



//zadanie
function guessNumber(attempts) {
  const target = Math.floor(Math.random() * 10) + 1; // число от 1 до 10

  for (let i = 0; i < attempts.length; i++) {
    if (attempts[i] === target) {
      return {
        success: true,
        attempt: i + 1,
        number: target
      };
    }
  }

  return {
    success: false,
    attemptsTried: attempts.length,
    number: target
  };
}

// Пример использования:
const result = guessNumber([3, 5, 2, 7]);
console.log(result);



//zadanie
class NumberStats {
  constructor(numbers) {
    this.numbers = numbers;
  }

  // Метод: длина списка
  getLength() {
    return this.numbers.length;
  }

  // Метод: среднее арифметическое
  getAverage() {
    if (this.numbers.length === 0) return 0;
    const sum = this.numbers.reduce((acc, val) => acc + val, 0);
    return sum / this.numbers.length;
  }
}

// Пример использования:
const stats = new NumberStats([5, 10, 15, 20]);

console.log("Długość listy:", stats.getLength());         // => 4
console.log("Średnia arytmetyczna:", stats.getAverage()); // => 12.5


//zadanie 4
function generateRandom(min, max) {
  return Math.floor(Math.random() * (max - min + 1) + min);
}

const numbers = [];
for (let i = 0; i < 10; i++) {
  numbers.push(generateRandom(1, 20));
}

console.log("Wylosowane liczby:", numbers);

const aboveTen = numbers.filter(n => n > 10).length;

if (aboveTen >= 5) {
  console.log("Udało się");
} else {
  console.log("Niestety nie");
}


//zadanie 5
function checkPalindrom(txt) {
  const cleaned = txt.toLowerCase().replace(/\s/g, '');
  const reversed = cleaned.split('').reverse().join('');
  return cleaned === reversed;
}

console.log(checkPalindrom("kajak"));      // true
console.log(checkPalindrom("Ala ma ala")); // true
console.log(checkPalindrom("kot"));        // false


//zadanie 6
function random(max) {
  return Math.floor(Math.random() * (max + 1));
}

const arr = [];
for (let i = 0; i < 20; i++) {
  arr.push(random(100));
}

arr.sort((a, b) => a - b);
console.log("Posortowana tablica:", arr);

const sum = arr.reduce((acc, val) => acc + val, 0);
const avg = sum / arr.length;

console.log("Suma:", sum);
console.log("Średnia:", avg.toFixed(2));


//zadanie 7
function removeDuplicates(nums) {
  if (nums.length === 0) return 0;

  let k = 1;
  for (let i = 1; i < nums.length; i++) {
    if (nums[i] !== nums[i - 1]) {
      nums[k] = nums[i];
      k++;
    }
  }
  return k;
}

const nums = [1, 1, 2, 2, 3, 4, 4];
const k = removeDuplicates(nums);
console.log("Liczba unikalnych:", k);
console.log("Unikalne elementy:", nums.slice(0, k));



//zadanie 8
function longestCommonPrefix(strs) {
  if (strs.length === 0) return "";

  let prefix = strs[0];

  for (let i = 1; i < strs.length; i++) {
    while (strs[i].indexOf(prefix) !== 0) {
      prefix = prefix.slice(0, -1);
      if (prefix === "") return "";
    }
  }
  return prefix;
}

console.log(longestCommonPrefix(["flower", "flow", "flight"])); // "fl"
console.log(longestCommonPrefix(["dog", "racecar", "car"]));    // ""


