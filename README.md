# README: Лабораторная работа №3. Использование хуков и рендер списков

## Инструкции по запуску проекта

### Требования

- Node.js (версия 16+)
- npm или yarn
- Браузер с поддержкой ES6

### Установка и запуск

1. Клонируйте репозиторий:
   ```sh
   git clone ...
   cd ...
   ```
2. Установите зависимости:
   ```sh
   npm install
   ```
3. Запустите проект:
   ```sh
   npm run dev
   ```
4. Откройте браузер и перейдите по адресу, указанному в консоли.

## Описание лабораторной работы

Этот проект представляет собой лабораторную работу по React, в которой используется `useState` и `useEffect` для управления состоянием и динамического рендеринга списков. В качестве примера реализован интернет-магазин одежды.

## Краткая документация к проекту

### Структура проекта

- `src/components/Header.jsx` – компонент заголовка.
- `src/components/Footer.jsx` – компонент подвала.
- `src/components/ProductCard.jsx` – карточка товара.
- `src/components/ProductList.jsx` – список товаров.
- `src/components/Slider.jsx` – слайдер изображений.
- `src/data/products.json` – тестовые данные для списка товаров.

### Основные технологии

- React (Vite)
- Хуки: `useState`, `useEffect`
- JSON для хранения мок-данных

## Примеры использования проекта

### Пример кода

#### Компонент карточки товара (`ProductCard.jsx`):
```jsx
import { useState } from "react";

function ProductCard({ product }) {
  const [selectedSize, setSelectedSize] = useState(null);

  const handleSizeChange = (size) => {
    setSelectedSize(size);
  };

  return (
    <div className="product-card">
      <img src={product.image} alt={product.name} />
      <h2>{product.name}</h2>
      <p>{product.description}</p>
      <p className="price">{product.price} лей</p>
      <div className="sizes">
        {product.sizes.map((size) => (
          <button
            key={size}
            onClick={() => handleSizeChange(size)}
            className={selectedSize === size ? "active" : ""}
          >
            {size}
          </button>
        ))}
      </div>
      <button className="add-to-cart">Добавить в корзину</button>
    </div>
  );
}

export default ProductCard;
```

#### Компонент списка товаров (`ProductList.jsx`):
```jsx
import { useState, useEffect } from "react";
import ProductCard from "./ProductCard";
import productsData from "../data/products.json";

function ProductList() {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    setProducts(productsData);
  }, []);

  return (
    <div>
      {products.map((product) => (
        <ProductCard key={product.id} product={product} />
      ))}
    </div>
  );
}

export default ProductList;
```

## Ответы на контрольные вопросы

1. **Как работает `useState`?**
   - `useState` используется для создания состояния внутри функционального компонента. Оно возвращает текущий `state` и функцию для его обновления.

2. **Как использовать `useEffect` для загрузки данных?**
   - `useEffect` с пустым массивом зависимостей (`[]`) выполняется один раз при монтировании компонента и используется для загрузки данных, подписок и других побочных эффектов.

3. **Как динамически рендерить списки в React?**
   - Используется метод `map()`, который проходит по массиву данных и возвращает JSX-разметку для каждого элемента.

## Список использованных источников

- [Официальная документация React](https://reactjs.org/)
- [Учебник по React на freeCodeCamp](https://www.freecodecamp.org/learn/front-end-libraries/react/)

## Дополнительные важные аспекты

- **Стилизация:** В проекте используются CSS-классы для стилизации компонентов.
- **Адаптивность:** Макет адаптирован для разных экранов.
- **Дополнительный функционал:** В `Slider.jsx` реализовано автоматическое переключение слайдов каждые 3 секунды с помощью `useEffect`.

