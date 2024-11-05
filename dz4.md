1) Какие бывают алгоритмы сортировок ? 
    - Пузырьковая сортировка: 
    Пузырьковая сортировка это простой алгоритм. Он проходит по массиву и каждую итерацию меняет положение соседних элементоа, если они стоят не в том порядке. Например [3,2,5,4] - алгоритм сперва переставит 3 и 2 местами. а потом 5 и 4. Имеет сложность О(n^2)
    -  Быстрая сортировка
    Самый эффективный алгоритм, который делит массив на две части относительно случайного элемента и сортирует обе части. Сперва находит все элемент больше заданного элемент, а потом элементы меньше этого элемента. имеет сложность О(n*log n)
    - Богосорт
    Не самый эффективный алгоритм сортировки) Идея заключается в случайном переставлении элементов, пока массив не окажется отсортированном. Сложность О(!n)
    - Сортировка слиянием
    Этот алгоритм делит массив на 2 половины (находит среднее и от него строит этии 2 части). Похожа на Быструю сортировку,  но в этом случае элемент не случаен. Имеет сложность О(n*log n)

2) Прочитать про "Операторы и выражения, циклы в JS"
3) Создать объект Person несколькими способами, после создать объект Person2, чтобы в нём были доступны методы объекта Person. Добавить метод logInfo чтоб он был доступен всем объектам.
    \\ const Person = {
        logInfo: function() {
            console.log(`Name: ${this.name} surname: ${this.surname}`);
        }
    }
    const person = Object.create(Person)
    person.name = "John"
    person.surname = "Johnson"

    const person2 = Object.create(Person)
    person2.name = "James"
    person2.surname = "Jameson"

    \\ function Person(name, surname) {
        this.name = name
        this.surname = surname
        }
        Person.prototype.logInfo = function() {
            console.log(`Name: ${this.name} surname: ${this.surname}`)
    }

    function Person2(name, surname) {
        Person.call(this, name, surname)
    }
    Person2.prototype = Object.create(Person.prototype)

    \\ class Person {
        constructor(name, surname) { 
            this.name = name
            this.surname = surname
        }

        logInfo() {
            console.log(`Name: ${this.name} surname: ${this.surname}`)
        }
    }

    class Person2 extends Person { 
        constructor(name, surname) { 
            super(name, surname)
        }
    }

4) Создать класс PersonThree c get и set для поля name и конструктором, сделать класс наследник от класса Person.
    \\ class Person {
      constructor(name) {
        this._name = name
      }

      get name() {
        return this._name
      }

      set name(value) {
        this._name = value
      }
    }

    class PersonThree extends Person {
      constructor(name) {
        super(name)
      }
    }

БОНУС: 
1) Написать функцию, которая вернет массив с первой парой чисел, сумма которых равна total:

arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
total = 13;
//result = [4, 9]

const firstSum = (arr, total) => {
    let result = null
    for (let i = 0; i < arr.length - 1; i++) {
        const el = arr[i]
        let prevSum = total - el
        if (arr.some((cur) => cur === prevSum)) {
            result = [el, prevSum]
            break
        }
  }
  return result
}

firstSum(arr,total)

2) Какая сложность у вашего алгоритма ?
Думаю О(n^2) - первая n за for и вторая n за метод some