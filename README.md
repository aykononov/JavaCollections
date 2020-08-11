<small>

## Java - каркас коллекций Collections Framework.
###### *Алгоритмы и структуры данных в Java*

<details><summary>Интерфейс List и класс ArrayList</summary>

><details><summary>Интерфейс List</summary>
> 
>*Интерфейс List* определяет, что это должен быть любой класс, реализующий данный интерфейс, который должен обеспечить конкретный набор методов, включая add, get, remove и еще около 20.
>
>Реализации ArrayList и LinkedList предоставляют эти методы, поэтому их можно использовать как взаимозаменяемые. Метод, написанный для работы с List, будет работать с ArrayList, LinkedList или любым другим объектом, который реализует List.
>
>Наиболее часто используемые методы интерфейса List:  
>* **void add(int index, E obj)**: добавляет в список по индексу index объект obj
>* **boolean addAll(int index, Collection<? extends E> col)**: добавляет в список по индексу index все элементы коллекции col. Если в результате добавления список был изменен, то возвращается true, иначе возвращается false
>* **E get(int index)**: возвращает объект из списка по индексу index
>* **int indexOf(Object obj)**: возвращает индекс первого вхождения объекта obj в список. Если объект не найден, то возвращается -1
>* **int lastIndexOf(Object obj)**: возвращает индекс последнего вхождения объекта obj в список. Если объект не найден, то возвращается -1
>* **ListIterator<E> listIterator()**: возвращает объект ListIterator для обхода элементов списка
>* **static <E> List<E> of(элементы)**: создает из набора элементов объект List
>* **E remove(int index)**: удаляет объект из списка по индексу index, возвращая при этом удаленный объект
>* **E set(int index, E obj)**: присваивает значение объекта obj элементу, который находится по индексу index
>* **void sort(Comparator<? super E> comp)**: сортирует список с помощью компаратора comp
>* **List<E> subList(int start, int end)**: получает набор элементов, которые находятся в списке между индексами start и end
>
></details>
>
>**Класс ArrayList** представляет простой список, аналогичный массиву, за исключением, того что количество элементов в нем не фиксировано.  
>Конструкторы *ArrayList*:
>```
>ArrayList(): создает пустой список
>ArrayList(Collection <? extends E> col): создает список, в который добавляются все элементы коллекции col
>ArrayList(int capacity): создает список, который имеет начальную емкость capacity
>```
>Емкость в ArrayList представляет размер массива, который будет использоваться для хранения объектов. При добавлении элементов фактически происходит перераспределение памяти - создание нового массива и копирование в него элементов из старого массива. Изначальное задание емкости ArrayList позволяет снизить подобные перераспределения памяти, тем самым повышая производительность.
>
>[ArrayListDemo - Пример класса ArrayList и его методов](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceList/ArrayListDemo.java "Посмотреть пример Java")  
>
>Мы можем свободно добавлять в объект ArrayList дополнительные объекты, в отличие от массива, однако в реальности ArrayList использует для хранения объектов опять же массив. По умолчанию данный массив предназначен для 10 объектов. Если в процессе программы добавляется гораздо больше, то создается новый массив, который может вместить в себя все количество. *Подобные перераспределения памяти уменьшают производительность*. Поэтому если мы точно знаем, что у нас список не будет содержать больше определенного количества элементов, например, 25, то мы можем сразу же явным образом установить это количество, в конструкторе:  
>```java
>ArrayList<String> users = new ArrayList<String>(25);
>```
>
>**Задача**:  
>Нужно заполнить два списка четными числами, первый от 4 до 20 с отступлением в 4.  
>Второй от 2 до 20 с отступлением в 2.  
>В первом списке результат должен быть: 4, 8, 12, 16, 20.  
>Во втором : 2, 4, 6, 8, 10, 12, 14, 16, 18, 20.  
>Далее удалить из коллекций те цифры которые не повторяются.  
>Таким образом во втором списке останутся те элементы, которые присутствуют в первом списке.  
>Резульат должен быть: 4, 8, 12, 16, 20.
>  
>[ArrayListNumber - Пример решения задачи с применением ArrayList](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceList/ArrayListNumber.java "Посмотреть пример Java")
>
</details>

<details><summary>Очереди и класс ArrayDeque</summary>

>*Очереди* представляют структуру данных, работающую по принципу FIFO (first in - first out). То есть элемент первым *добавлен* в коллекцию и первым он из нее *удаляется*. Это стандартная модель *однонаправленной* очереди. Также бывают и *двунаправленные* - это такие очереди, в которых мы можем добавить элемент как в *начало* коллекции, так и в *конец*. Такиим же образом можем удалить элемент не только в конце коллекции, но и в начале.
>
>Особенностью классов очередей является то, что они реализуют специальные интерфейсы *Queue* или *Deque*.
>
><details><summary>Интерфейс Queue</summary>
>  
>Обобщенный интерфейс Queue<E> расширяет базовый интерфейс Collection и определяет поведение класса в качестве *однонаправленной* очереди. Свою функциональность он раскрывает через следующие методы:  
>* **E element()**: возвращает, но не удаляет, элемент из начала очереди. Если очередь пуста, генерирует исключение NoSuchElementException
>* **boolean offer(E obj)**: добавляет элемент obj в конец очереди. Если элемент удачно добавлен, возвращает true, иначе - false  
>* **E peek()**: возвращает без удаления элемент из начала очереди. Если очередь пуста, возвращает значение null  
>* **E poll()**: возвращает с удалением элемент из начала очереди. Если очередь пуста, возвращает значение null  
>* **E remove()**: возвращает с удалением элемент из начала очереди. Если очередь пуста, генерирует исключение NoSuchElementException  
>
>Таким образом, у всех классов, которые реализуют данный интерфейс, будет метод *offer* для добавления в очередь, метод *poll* для извлечения элемента из *начала* очереди, и методы *peek* и *element*, позволяющие просто *получить* элемент из начала очереди.
></details>
>
><details><summary>Интерфейс Deque</summary>
>  
>Интерфейс *Deque* расширяет вышеописанный интерфейс *Queue* и определяет поведение *двунаправленной очереди*, которая работает как обычная однонаправленная очередь, либо как *стек*, действующий по принципу LIFO (последний вошел - первый вышел).  
>Интерфейс Deque определяет следующие методы:  
>* **void addFirst(E obj)**: добавляет элемент в начало очереди  
>* **void addLast(E obj)**: добавляет элемент obj в конец очереди  
>* **E getFirst()**: возвращает без удаления элемент из головы очереди. Если очередь пуста, генерирует исключение NoSuchElementException  
>* **E getLast()**: возвращает без удаления последний элемент очереди. Если очередь пуста, генерирует исключение NoSuchElementException  
>* **boolean offerFirst(E obj)**: добавляет элемент obj в самое начало очереди. Если элемент удачно добавлен, возвращает true, иначе - false  
>* **boolean offerLast(E obj)**: добавляет элемент obj в конец очереди. Если элемент удачно добавлен, возвращает true, иначе - false  
>* **E peekFirst()**: возвращает без удаления элемент из начала очереди. Если очередь пуста, возвращает значение null  
>* **E peekLast()**: возвращает без удаления последний элемент очереди. Если очередь пуста, возвращает значение null  
>* **E pollFirst()**: возвращает с удалением элемент из начала очереди. Если очередь пуста, возвращает значение null  
>* **E pollLast()**: возвращает с удалением последний элемент очереди. Если очередь пуста, возвращает значение null  
>* **E pop()**: возвращает с удалением элемент из начала очереди. Если очередь пуста, генерирует исключение NoSuchElementException  
>* **void push(E element)**: добавляет элемент в самое начало очереди  
>* **E removeFirst()**: возвращает с удалением элемент из начала очереди. Если очередь пуста, генерирует исключение NoSuchElementException  
>* **E removeLast()**: возвращает с удалением элемент из конца очереди. Если очередь пуста, генерирует исключение NoSuchElementException  
>* **boolean removeFirstOccurrence(Object obj)**: удаляет первый встреченный элемент obj из очереди. Если удаление произшло, то возвращает true, иначе возвращает false  
>* **boolean removeLastOccurrence(Object obj)**: удаляет последний встреченный элемент obj из очереди. Если удаление произшло, то возвращает true, иначе возвращает false  
>
>Таким образом, наличие методов *pop* и *push* позволяет классам, реализующим этот элемент, действовать в качестве *стека*. В тоже время имеющийся функционал также позволяет создавать *двунаправленные очереди*, что делает классы, применяющие данный интерфейс, довольно гибкими.
>
></details>
>
>**Класс ArrayDeque**
>
>Класс *ArrayDeque<E>* представляет обобщенную двунаправленную очередь, наследуя функционал от класса AbstractCollection и применяя интерфейс Deque.
>В классе ArrayDeque определены следующие конструкторы:  
>```java
>ArrayDeque(): создает пустую очередь
>ArrayDeque(Collection<? extends E> col): создает очередь, наполненную элементами из коллекции col
>ArrayDeque(int capacity): создает очередь с начальной емкостью capacity. 
>```  
>Если мы явно не указываем начальную емкость, то емкость по умолчанию будет равна 16.
>
>[ArrayDequeDemo - Пример использования ArrayDequeDemo](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceList/ArrayDequeDemo.java "Посмотреть пример Java")
>
</details>


</small>