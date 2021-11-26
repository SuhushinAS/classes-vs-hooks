# Хуки VS Классы

- [Разбор Мотивации](#Разбор-Мотивации)
- [Сравнение кода](#Сравнение-кода)

## Разбор Мотивации

- Трудно повторно использовать логику состояний между компонентами
  - Компонент с привязанным состоянием нельзя использовать в другом контексте.
  - В любом случае получение данных нужно отделять от представления (Контейнеры/Компоненты).
- Сложные компоненты становятся трудными для понимания
  - Не понятно, чем здесь могут помочь хуки?
    - Сложный компонент на хуках, также труден для понимания.
    - Части кода в классе можно выделять в методы и группировать связанные части.
    - В функциональном компоненте код нельзя свободно перемещать, поскольку это всё часть тела функции.
- Классы путают как людей, так и машины
  - (Тут нужен какой-нибудь мем.)
  - Классы и this - это стандарт языка, которые нужно понимать.
  - Хуки "заметают грязь под ковёр": можно не думать про this, но надо помнить про замыкания и пересоздание объектов, а это ещё сложнее.
  - "Естественный барьер": Если разработчик не понимает this, то он и не должен разрабатывать важные части приложения.

## Сравнение кода

- Reference
  - Хуки
    ```javascript
    const FnComponent = (props) => {
      const ref = userRef(initValue);

      const someMethod = () => {
        ref.current = newValue;
      };
    }
    ```
  - Классы
    ```javascript
    class ClassComponent extends React.Component {
      ref = initValue;

      someMethod() {
        this.ref = newValue;
      }
    }
    ```
- State
  - Хуки
    ```javascript
    const FnComponent = (props) => {
      const [state, setState] = useState(initValue);

      const someMethod = () => {
        setState(newValue);
      };
    }
    ```
  - Классы
    ```javascript
    class ClassComponent extends React.Component {
      state = initValue;

      someMethod() {
        this.setState(newValue);
      }
    }
    ```
- Callbacks
  - Хуки
    ```javascript
    const FnComponent = (props) => {
      const callback = useCallback(
        () => {
          // code
        },
        [...dependecyList]
      );

      return <button onClick={callback}>Push me</button>;
    }
    ```
  - Классы
    ```javascript
    class ClassComponent extends React.Component {
      callback = () => {
        // code
      };

      render() {
        return <button onClick={this.callback}>Push me</button>;
      }
    }
    ```
