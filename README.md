<!DOCTYPE html>
<html lang="en">

<head>
  <title>Web Sprint 3 Challenge</title>
  <style>
    * {
      font-family: 'Times New Roman', Times, serif
    }

    .widget {
      padding: 0 0 0.5rem 0.65rem;
      margin-bottom: 0.5rem;
      border: 1px solid black;
      border-radius: 0.5rem;
    }

    .widget p {
      font-style: italic;
    }

  </style>
</head>

<body>
  <h1>Web Sprint 3 Challenge </h1>
  <p>❗ See the last script tag for instructions on completing your Challenge</p>
  <!-- widgets start, do not modify -->
  <section class="widget">
    <p>This widget uses the EBook class</p>
    <textarea placeholder="Write your book"></textarea><br />
    <input type="number" placeholder="Characters per page" /><br /><br />
    <button id="turnPage">Turn Page</button>
    <p id="bookPage"></p>
  </section>
  <!-- widgets end -->

  <!-- The first script tag loads a library called lodash that helps with testing -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.21/lodash.min.js"></script>
  <script id="challenge">
    // In CHALLENGES 1-4 you will write JavaScript classes

    // ❗ Do not rename the classes provided
    // ❗ Do not alter the position of the script tags
    // ❗ Debug properly using the Console

    

// 👉 CHALLENGE 1 - Integers
class Integers {
  constructor(...args) {
    this.ints = [...args];
  }

  getAll() {
    return this.ints;
  }

  getEvens() {
    return this.ints.filter(num => num % 2 === 0);
  }

  getNegatives() {
    return this.ints.filter(num => num < 0);
  }

  getAllSquared() {
    return this.ints.map(num => num * num);
  }

  pop() {
    return this.ints.pop();
  }

  push(num) {
    this.ints.push(num);
    return this.ints;
  }

  getEveryNth(n) {
    return this.ints.filter((_, index) => index % n === 0);
  }

  getAllReversed() {
    return this.ints.slice().reverse();
  }
}

// 👉 CHALLENGE 2 - NerfGun
class NerfGun {
  constructor(totalProjectiles) {
    this.maxCapacity = totalProjectiles;
    this.currentCapacity = totalProjectiles;
    this.safetyOn = true;
  }

  shoot() {
    if (this.currentCapacity > 0 && !this.safetyOn) {
      this.currentCapacity--;
      return "Bang!";
    } else {
      return "Click!";
    }
  }

  reload(number) {
    if (typeof number !== "number" || number <= 0) {
      return "Error reloading!";
    } else {
      this.currentCapacity = Math.min(this.maxCapacity, this.currentCapacity + number);
      return `${this.currentCapacity} projectiles left!`;
    }
  }

  toggleSafety() {
    this.safetyOn = !this.safetyOn;
    return this.safetyOn ? "Safety enabled!" : "Safety disabled!";
  }
}

// 👉 CHALLENGE 3 - EBook
class EBook {
  constructor(text, pageSize) {
    this.text = text;
    this.pageSize = pageSize;
    this.currentPage = 0;
  }

  next() {
    const nextPage = this.text.slice(this.currentPage, this.currentPage + this.pageSize);
    this.currentPage += this.pageSize;
    return nextPage.length > 0 ? nextPage : null;
  }
}

// 👉 CHALLENGE 4 - AntFarm
class AntFarm {
  constructor(...ants) {
    this.ants = ants.map(name => ({ name, health: 100 }));
  }

  work() {
    if (this.ants.length === 0) {
      return "No ants here. Did you work them to death?";
    }
    this.ants.forEach(ant => {
      ant.health -= 20;
      if (ant.health <= 0) {
        this.ants.splice(this.ants.indexOf(ant), 1);
      }
    });
    return `${this.ants.length} ants starting work!`;
  }

  feed(name) {
    const ant = this.ants.find(ant => ant.name === name);
    if (ant) {
      ant.health += 15;
      return "Yum!";
    } else {
      return `${name} not found!`;
    }
  }
}

    // 🧪 TESTS, do not make any changes below this line ===================
    // 🧪 TESTS, do not make any changes below this line ===================
    // 🧪 TESTS, do not make any changes below this line ===================
    globalThis.challengeVersion = 1
    globalThis.Integers = Integers
    globalThis.NerfGun = NerfGun
    globalThis.EBook = EBook
    globalThis.AntFarm = AntFarm

    try {
      testClass('CHALLENGE 1 - class Integers', [
        function () {
          let actual, description = 'getAll returns all the ints'
          let expected = [1, 2, 3, 4]
          try {
            const ints = new Integers(1, 2, 3, 4)
            actual = ints.getAll()
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'getEvens returns the even ints'
          let expected = [0, 2, 4]
          try {
            const ints = new Integers(0, 2, 3, 5, 4)
            actual = ints.getEvens()
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'getNegatives returns the negative ints'
          let expected = [-3, -5]
          try {
            const ints = new Integers(-3, 5, -5, 0)
            actual = ints.getNegatives()
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'getAllSquared returns the ints squared'
          let expected = [4, 1, 0, 36, 25]
          try {
            const ints = new Integers(2, 1, 0, 6, 5)
            actual = ints.getAllSquared()
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'pop removes the last int and returns it'
          let expected = [3, [1, 2]]
          try {
            const ints = new Integers(1, 2, 3)
            actual = []
            actual.push(ints.pop())
            actual.push(ints.ints)
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'push adds an integer into ints and returns the updated ints'
          let expected = [[1, 2, 3, 4], [1, 2, 3, 4]]
          try {
            const ints = new Integers(1, 2, 3)
            actual = []
            actual.push(ints.push(4))
            actual.push(ints.ints)
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'getEveryNth returns ints at every nth index'
          let expected = [[1, 3, 5], [1, 4]]
          try {
            const ints = new Integers(1, 2, 3, 4, 5, 6)
            actual = []
            actual.push(ints.getEveryNth(2))
            actual.push(ints.getEveryNth(3))
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'getAllReversed returns the ints in reverse order'
          let expected = [[6, 5, 4, 3, 2, 1], [0, 1, 9, 3, 6, 9]]
          try {
            const ints = new Integers(1, 2, 3, 4, 5, 6)
            const ints2 = new Integers(9, 6, 3, 9, 1, 0)
            actual = []
            actual.push(ints.getAllReversed())
            actual.push(ints2.getAllReversed())
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
      ])
      testClass('CHALLENGE 2 - class NerfGun', [
        function () {
          let actual, description = 'A new NerfGun has its safety on'
          let expected = "Click!"
          try {
            const nerf = new NerfGun(6)
            actual = nerf.shoot()
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'A NerfGun can disable safety, shoot, re-enable safety'
          let expected = ["Safety disabled!", "Bang!", "Safety enabled!", "Click!"]
          try {
            const nerf = new NerfGun(6)
            actual = []
            actual.push(nerf.toggleSafety())
            actual.push(nerf.shoot())
            actual.push(nerf.toggleSafety())
            actual.push(nerf.shoot())
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'A NerfGun can not shoot after running out of projectiles'
          let expected = ["Bang!", "Bang!", "Bang!", "Click!"]
          try {
            const nerf = new NerfGun(3)
            nerf.toggleSafety()
            actual = []
            actual.push(nerf.shoot()); actual.push(nerf.shoot()); actual.push(nerf.shoot()); actual.push(nerf.shoot())
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'A NerfGun can be reloaded to less than capacity'
          let expected = ["2 projectiles left!", "Bang!", "Bang!", "Click!"]
          try {
            const nerf = new NerfGun(3)
            nerf.toggleSafety()
            nerf.shoot()
            nerf.shoot()
            nerf.shoot()
            actual = []
            actual.push(nerf.reload(2))
            actual.push(nerf.shoot()); actual.push(nerf.shoot()); actual.push(nerf.shoot())
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'Reloading to more than capacity only fills NerfGun to capacity'
          let expected = ["3 projectiles left!", "Bang!", "Bang!", "Bang!", "Click!"]
          try {
            const nerf = new NerfGun(3)
            nerf.toggleSafety()
            nerf.shoot()
            actual = []
            actual.push(nerf.reload(100))
            actual.push(nerf.shoot()); actual.push(nerf.shoot())
            actual.push(nerf.shoot()); actual.push(nerf.shoot())
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'Reloading NerfGun incorrectly yields an error message'
          let expected = ["Error reloading!", "Error reloading!", "Error reloading!"]
          try {
            const nerf = new NerfGun(6)
            actual = []
            actual.push(nerf.reload(0))
            actual.push(nerf.reload(-1))
            actual.push(nerf.reload('5'))
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
      ])
      testClass('CHALLENGE 3 - class EBook', [
        function () {
          let actual, description = 'Ebook can turn pages'
          let expected = ['abc', 'def', 'g']
          try {
            const book = new EBook('abcdefg', 3)
            actual = []
            actual.push(book.next()); actual.push(book.next()); actual.push(book.next())
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'Turning page yields null when there is no more text'
          let expected = ['abcd', 'efgh', 'ij', null, null]
          try {
            const book = new EBook('abcdefghij', 4)
            actual = []
            actual.push(book.next()); actual.push(book.next()); actual.push(book.next())
            actual.push(book.next()); actual.push(book.next())
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
      ])
      testClass('CHALLENGE 4 - class AntFarm', [
        function () {
          let actual, description = 'AntFarm initializes the ants correctly'
          let expected = [
            { name: 'Jess', health: 100 }, { name: 'Blake', health: 100 }, { name: 'Jess', health: 100 }
          ]
          try {
            const farm = new AntFarm('Jess', 'Blake', 'Jess')
            actual = farm.ants
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'Working substracts 20 health points'
          let expected = [
            { name: 'Jess', health: 80 }, { name: 'Blake', health: 80 }, { name: 'Jess', health: 80 }
          ]
          try {
            const farm = new AntFarm('Jess', 'Blake', 'Jess')
            farm.work()
            actual = farm.ants
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'Overworking kills the ants'
          let expected = []
          try {
            const farm = new AntFarm('Jess', 'Blake', 'Jess')
            farm.work(); farm.work(); farm.work(); farm.work(); farm.work()
            actual = farm.ants
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'Working returns the correct string'
          let expected = ["3 ants starting work!", "1 ants starting work!", "No ants here. Did you work them to death?"]
          try {
            const farm = new AntFarm('Jess', 'Blake', 'Jess')
            farm.ants[0].health++
            actual = []
            farm.work(); farm.work(); farm.work(); farm.work()
            actual.push(farm.work()); actual.push(farm.work()); actual.push(farm.work())
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'Feeding increases 15 health points of lucky ant(s)'
          let expected = [{ name: "Jess", "health": 115 }, { name: "Blake", health: 100 }, { name: "Jess", health: 115 }]
          try {
            const farm = new AntFarm('Jess', 'Blake', 'Jess')
            farm.feed('Jess')
            actual = farm.ants
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
        function () {
          let actual, description = 'Feeding returns the correct string'
          let expected = ["Yum!", "bad name not found!", "another bad name not found!"]
          try {
            const farm = new AntFarm('Jess', 'Blake', 'Jess')
            actual = []
            actual.push(farm.feed('Blake'))
            actual.push(farm.feed('bad name'))
            actual.push(farm.feed('another bad name'))
          } catch (err) { actual = err.message }
          return [description, expected, actual]
        },
      ])
      function testClass(testTitle, tests) {
        console.log(testTitle)
        tests.forEach((test, idx) => {
          const [, expected, actual] = test()
          const [desJSON, expJSON, actJSON] = test().map(JSON.stringify)
          if (_.isEqual(expected, actual)) {
            console.log(`\t✅ Test ${idx + 1} ${desJSON} PASSED`)
          } else {
            console.log(`\t❌ Test ${idx + 1} ${desJSON} FAILED:
              Expected ${expJSON}
              Actual   ${actJSON}`)
          }
        })
      }
      let getTextArea = () => document.querySelector('.widget textarea')
      let getNumberInput = () => document.querySelector('.widget input[type=number]')
      const getText = () => getTextArea().value
      const getChars = () => Number(getNumberInput().value)
      turnPage.disabled = true
      let book
      let updateBook = () => {
        turnPage.disabled = (getText() && getChars() && getChars() > 0) ? false : true
        book = new EBook(getText(), getChars())
      }
      getTextArea().oninput = updateBook
      getNumberInput().oninput = updateBook
      turnPage.onclick = () => {
        bookPage.textContent = book.next() || 'The End'
      }
    } catch (err) { console.error(err.stack) }
  </script>
</body>

</html>
