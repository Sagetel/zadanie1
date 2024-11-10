1. 
let promiseTwo = new Promise((resolve, reject) => {
   resolve("a");
});

promiseTwo
.then((res) => {
   return res + "b";
})
.then((res) => {
   return res + "с";
})
.finally((res) => {
   return res + "!!!!!!!";
})
.catch((res) => {
   return res + "d";
})
.then((res) => {
   console.log(res);
});

\\ Выведет abc. Отработают два первых then (abс). finally ничего не принимает и не изменит res. catch не отработает, потому что ошибки нет. И отработает последний then -> выведет сообщенеи в консоль

2. 
function doSmth() {
   return Promise.resolve("123");
}

doSmth()
.then(function (a) {
   console.log("1", a); // 1, 123
   return a;
})
.then(function (b) {
   console.log("2", b);
   return Promise.reject("321"); 2, 123
})
.catch(function (err) {
   console.log("3", err); 3, 321
})
.then(function (c) {
   console.log("4", c); 4, undefined 
return c;
});

Первый then выведет 1, 123. После вернет 123 для следующего then, который выведет 2, 123 и вернет reject с 321. Далее отработает catch, потому что предыдущий then вернул ошибку. В следующий then попадет значение undefined, потому что в catch пропущен return. Последний then выведет 4, undefined 

3. Напишите функцию, которая будет проходить через массив целых чисел и выводить индекс каждого элемента с задержкой в 3 секунды.
Входные данные: [10, 12, 15, 21]

const logger = async (arr) => {
   for (let i = 0; i < arr.length; i++) {
      await new Promise((resolve) => {
         setTimeout(() => {
            console.log(i)
            resolve()
         }, 3000)
      })
   }
}

logger([10, 12, 15, 21])

4. Прочитать про Top Level Await (можно ли использовать await вне функции async) \\ +

БОНУС ЗАДАНИЕ 
/* Необходимо реализовать функцию fetchUrl, которая будет использоваться следующим образом.
Внутри fetchUrl можно использовать условный метод fetch, который просто возвращает
Promise с содержимым страницы или вызывает reject */
fetchUrl('https://google/com&#39;)
.then(...)
.catch(...) // сatch должен сработать только после 5 неудачных попыток
получить содержимое страницы внутри fetchUrl

const fetchUrl  = (url, counter = 5) => {
    return fetch(url)
    .then((response)=> {
        if(response.ok) {
            return response.json()
        } else {
            return Promise.reject(response);
        }
    })
    .catch((error)=>{
        if (counter > 0) {
            return fetchUrl(url, counter-1)
        } else {
            return Promise.reject(error)
        }
    })
}

fetchUrl('https://google/com&#39;')
.then(...)
.catch(...) //