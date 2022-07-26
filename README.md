# Небольшая веб-страница, написанная с помощью HTML и CSS

## Содержание

1. [Сайт "Далекий космос", описывающий масштабы вселенной](#сайт)
2. [Функциональность сайта](#функциональность)
3. [Основные моменты при реализации](#реализация)  
    3.1 [Страница scale.html](#scale)

<a name="сайт"></a>
## Сайт "Далекий космос", описывающий масштабы вселенной

Сам сайт состоит из трех страниц, рассказывающих о масштабах вселенной и нашем месте в ней, объектах Солнечной системы и космических аппаратах.

При открытии сайта открывается страница _"Масштабы"_ далее с нее возможен переход на другие страницы _"Планеты"_ и _"Космические аппараты"_. Открытие всех страниц начинается с загрузки, которая плавно перетекает в заголовок. Внизу всех страниц находятся кнопка "Наверх" и блок с ссылками для переходов на другие страницы.

Сайт доступен по ссылке:

<a name="функциональность"></a>
## Функциональность сайта

На всех страницах реализована анимация заголовка и анимация при скролле. На странице "Масштабы" в последнем блоке реализована анимация 8-ми картинок, показывающих масштабы вселенной.

Основная идея и некоторая информация для сайта "Масштабы" взята из [статьи](https://zen.yandex.ru/media/id/61118a9e252a7425afc22df9/razmery-nashei-zemli-k-masshtabam-vselennoi-6117e93c74a4fa1687d0764e) и [статьи](https://mrvorchun.livejournal.com/3123909.html?noscroll).

<a name="реализация"></a>
## Основные моменты при реализации

Для расположения объектов по горизонтали использовались каскадные таблица стилей.

```html
<!--Ссылки на другие страницы-->
<div class="links">
  <a class="link" href="planets.html">Планеты</a>
  <a class="link" href="spacecrafts.html">Космические аппараты</a>
</div>
```

```CSS
/*Ссылки на другие страницы*/
.links {
  width: 100%;
  text-align: center;
  ...
}

.links .link {
  position: relative;
  width: 25%;
  display: inline-block;
  ...
}
```

<a name="scale"></a>
### Страница scale.html

Анимация загрузки страницы реализована с помощью трех блоков _div_ имеющих круглую форму.

```html
<!--Начальная заставка-->
<div id="circles">
  <div class="circle"></div>
  <div class="circle"></div>
  <div class="circle"></div>
</div>
```

Для корректной загрузки была реализована функция задержки.

```js
//Функция задержки
function sleep(ms)
{
  return new Promise(
    resolve => setTimeout(resolve, ms)
  );
}
```

Сама анимация реализована с помощью скрипта с трехкратным добавлением и удалением класса _active_ к элементам загрузки.

```js
//Начальная заставка
async function animHead()
{
  //Анимация точек в начале
  const circles = document.querySelectorAll('.circle');

  //Трехкратное добавление и удаление класса active
  for(let i = 0; i < 3; i++)
  {
    circles[0].classList.add('active');
    circles[1].classList.remove('active');
    circles[2].classList.add('active');
    //Задержка между анимацией
    await sleep(300);
    circles[0].classList.remove('active');
    circles[1].classList.add('active');
    circles[2].classList.remove('active');
    //Задержка между анимацией
    await sleep(300);
  }

  //Маскировка элементов загрузки
  document.getElementById('circles').classList.add("noactive");
  //Появление основных объектов заголовка
  const head = document.querySelectorAll('header');
  head[0].classList.remove('active');
}
```

[Карликовые планеты](https://spacegid.com/poyas-koypera.html#i-8)
