1) Написать ответ - почему массивы в JS являются "неправильными" и совмещают в себе несколько структур данных? Какие?
Массивы в js являются неправильными по ряду причин:
    - Элементами одного массива могут быть данные любого типа. Один массив может включать в себя как числа, строки, так и булево, массивы и т. д.
    - Массивы могут выступать в роли объекта, поскольку позволяют указывать строки в качестве индекса элемента
    - Также длина массива не фиксирована, в отличие от других языков
Учитывая эти особенности, можно сказать, что массив совмещает в себе следующие структуры данных: 
    - хэш-таблицы (объект)
    - стек (включает в себя методы push()/pop(). Позволять извлечь элемент по индексу -- метод splice())
    - Очередь (Методы push() и shift() позволяют реализовать функционал очереди)
    - Дерево (так как массив может быть многомерным)
2) Привязать контекст объекта к функции logger, чтобы при вызове this.item выводило - some value (Привязать через bind, call, apply)
    function logger() {
        console.log(`I output only external context: ${this.item}`);
    }
    const obj = { item: "some value" };

    \\ const bindContex = logger.bind(obj); bindContex()
    \\ logger.call(obj);
    \\ logger.apply(obj);
3) 
    1) Массивы:
    - Создайте массив чисел и найдите его сумму.
        const array = [1,23,24,3,2423,4]
        const result = array.reduce((acc, cur)=>acc+=cur, 0)

    - Создайте массив строк и объедините их в одну строку.
        const array = ['I ', 'know ', 'H.', 'T.', 'M.', 'L']
        \\ const str = array.join('')
        \\ const result = array.reduce((acc, cur)=>acc+=cur,'')

    - Найдите максимальный и минимальный элементы в массиве чисел.
        const array = [1, 2, 3, 4, 100, 5, 6, 7, 8, 9, 0]
        const sortedArray = array.toSorted((a, b) => a - b)
        const [minValue, maxValue] = [sortedArray[0], sortedArray[sortedArray.length-1]]
    2) Stack (стек):
    - Реализуйте стек с использованием массива.
     function stackConstructor() {
      this.values = []
      this.copyValues = []
      this.add = (el) => {
        this.copyValues = [...this.values]
        this.values.push(el)
      }
      this.getForced = () => {
        this.copyValues = [...this.values]
        const el = this.values.pop()
        return el
      }
      this.get = () => {
        return this.values[this.values.length-1]
      }
      this.undo = () => {
        this.values = this.copyValues
      }
      this.isEmpty = () => {
        return !Boolean(this.values.length)
      }
    }
    const megaStack = new stackConstructor()
    megaStack.add(1)
    megaStack.add(10)
    megaStack.undo()
    megaStack.add(100)
    console.log(megaStack.getForced(), megaStack.getForced(), megaStack.isEmpty()) // 100 1 true

    3) Queue (очередь):

    - Реализуйте очередь с использованием массива.
    - Имитируйте работу очереди на примере ожидания на кассе.
    function queueConstructor() {
        this.values = []
        this.add = (el) => {
          this.values.push(el)
        }
        this.getForced = () => {
          const el = this.values.shift()
          return el
        }
        this.get = () => {
          return this.values[0]
        }
        this.isEmpty = () => {
        return !Boolean(this.values.length)
      }
    }

    const megaQueue = new queueConstructor()
    megaQueue.add('John')
    megaQueue.add("Maria")
    megaQueue.add("Mark")
    console.log(megaQueue.getForced(), megaQueue.getForced(), megaQueue.getForced(), megaQueue.isEmpty()) // John Maria Mark true
    
    Бонус задание: Реализовать полифил(собственную функцию реализующую встроенную в js) метода bind()
    - 
    function logger(name, age) {
        console.log(`I output only external context: ${this.item} + ${name} + ${age}`);
    }
    Function.prototype.myBind = function (context, ...args) {
      const func = this
      return function(...newArgs) {
        return func.call(context, ...newArgs.concat(...args))

      }
    }
    const obj = { item: "some value" };
    const loggerBined = logger.myBind(obj, 'John', 18) \\ john и 18 Добавил для проверки возможности передачи аргементов
    loggerBined()