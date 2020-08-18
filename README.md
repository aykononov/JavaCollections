<small>

## Примеры использования коллекций и принципы их работы.
## Examples of using collections and how they work.

###### *Java Collections Framework - каркас коллекций*

<details><summary>Интерфейс List и класс ArrayList</summary>

><details><summary>Интерфейс List</summary>
> 
>**Интерфейс List**
>
>Определяет, что это должен быть любой класс, реализующий данный интерфейс, который должен обеспечить конкретный набор методов, включая add, get, remove и еще около 20.
>
>Реализации ArrayList и LinkedList предоставляют эти методы, поэтому их можно использовать как взаимозаменяемые. Метод, написанный для работы с List, будет работать с ArrayList, LinkedList или любым другим объектом, который реализует List.
>
>Наиболее часто используемые методы интерфейса List:
>```  
> void add(int index, E obj): добавляет в список по индексу index объект obj
> boolean addAll(int index, Collection<? extends E> col): добавляет в список по индексу index все элементы коллекции col. Если в результате добавления список был изменен, то возвращается true, иначе возвращается false
> E get(int index): возвращает объект из списка по индексу index
> int indexOf(Object obj): возвращает индекс первого вхождения объекта obj в список. Если объект не найден, то возвращается -1
> int lastIndexOf(Object obj): возвращает индекс последнего вхождения объекта obj в список. Если объект не найден, то возвращается -1
> ListIterator<E> listIterator(): возвращает объект ListIterator для обхода элементов списка
> static <E> List<E> of(элементы): создает из набора элементов объект List
> E remove(int index): удаляет объект из списка по индексу index, возвращая при этом удаленный объект
> E set(int index, E obj): присваивает значение объекта obj элементу, который находится по индексу index
> void sort(Comparator<? super E> comp): сортирует список с помощью компаратора comp
> List<E> subList(int start, int end): получает набор элементов, которые находятся в списке между индексами start и end
>```
>
></details>
>
>**Класс ArrayList** 
>
>Класс *ArrayList* - представляет простой список, аналогичный массиву, за исключением, того что количество элементов в нем не фиксировано.  
>Конструкторы *ArrayList*:
>```
>ArrayList(): создает пустой список
>ArrayList(Collection <? extends E> col): создает список, в который добавляются все элементы коллекции col
>ArrayList(int capacity): создает список, который имеет начальную емкость capacity
>```
>Емкость в ArrayList представляет размер массива, который будет использоваться для хранения объектов. При добавлении элементов фактически происходит перераспределение памяти - создание нового массива и копирование в него элементов из старого массива. Изначальное задание емкости ArrayList позволяет снизить подобные перераспределения памяти, тем самым повышая производительность.
>
>[ArrayListDemo - Пример использования класса ArrayList и его методов](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceList/ArrayListDemo.java "Посмотреть пример Java")  
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
>[ArrayListExample - Задача с применением ArrayList](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceList/ArrayListExample.java "Посмотреть пример Java")
>
</details>

<details><summary>Очереди и класс ArrayDeque</summary>

>*Очереди* представляют структуру данных, работающую по принципу FIFO (first in - first out). То есть элемент первым *добавлен* в коллекцию и первым он из нее *удаляется*. Это стандартная модель *однонаправленной* очереди. Также бывают и *двунаправленные* - это такие очереди, в которых мы можем добавить элемент как в *начало* коллекции, так и в *конец*. Такиим же образом можем удалить элемент не только в конце коллекции, но и в начале.
>
>Особенностью классов очередей является то, что они реализуют специальные интерфейсы *Queue* или *Deque*.
>
><details><summary>Обобщенный интерфейс Queue<E></summary>
>  
>Расширяет базовый интерфейс Collection и определяет поведение класса в качестве *однонаправленной* очереди. 
>
>Свою функциональность он раскрывает через следующие методы:
>```  
> E element(): возвращает, но не удаляет, элемент из начала очереди. Если очередь пуста, генерирует исключение NoSuchElementException
> boolean offer(E obj): добавляет элемент obj в конец очереди. Если элемент удачно добавлен, возвращает true, иначе - false  
> E peek(): возвращает без удаления элемент из начала очереди. Если очередь пуста, возвращает значение null  
> E poll(): возвращает с удалением элемент из начала очереди. Если очередь пуста, возвращает значение null  
> E remove(): возвращает с удалением элемент из начала очереди. Если очередь пуста, генерирует исключение NoSuchElementException  
>```
>
>Таким образом, у всех классов, которые реализуют данный интерфейс, будет метод *offer* для добавления в очередь, метод *poll* для извлечения элемента из *начала* очереди, и методы *peek* и *element*, позволяющие просто *получить* элемент из начала очереди.
></details>
>
><details><summary>Интерфейс Deque</summary>
>
>Расширяет вышеописанный интерфейс *Queue* и определяет поведение *двунаправленной очереди*, которая работает как обычная однонаправленная очередь, либо как *стек*, действующий по принципу LIFO (последний вошел - первый вышел).  
>
>Интерфейс Deque определяет следующие методы:
>```  
> void addFirst(E obj): добавляет элемент в начало очереди  
> void addLast(E obj): добавляет элемент obj в конец очереди  
> E getFirst(): возвращает без удаления элемент из головы очереди. Если очередь пуста, генерирует исключение NoSuchElementException  
> E getLast(): возвращает без удаления последний элемент очереди. Если очередь пуста, генерирует исключение NoSuchElementException  
> boolean offerFirst(E obj): добавляет элемент obj в самое начало очереди. Если элемент удачно добавлен, возвращает true, иначе - false  
> boolean offerLast(E obj): добавляет элемент obj в конец очереди. Если элемент удачно добавлен, возвращает true, иначе - false  
> E peekFirst(): возвращает без удаления элемент из начала очереди. Если очередь пуста, возвращает значение null  
> E peekLast(): возвращает без удаления последний элемент очереди. Если очередь пуста, возвращает значение null  
> E pollFirst(): возвращает с удалением элемент из начала очереди. Если очередь пуста, возвращает значение null  
> E pollLast(): возвращает с удалением последний элемент очереди. Если очередь пуста, возвращает значение null  
> E pop(): возвращает с удалением элемент из начала очереди. Если очередь пуста, генерирует исключение NoSuchElementException  
> void push(E element): добавляет элемент в самое начало очереди  
> E removeFirst(): возвращает с удалением элемент из начала очереди. Если очередь пуста, генерирует исключение NoSuchElementException  
> E removeLast(): возвращает с удалением элемент из конца очереди. Если очередь пуста, генерирует исключение NoSuchElementException  
> boolean removeFirstOccurrence(Object obj): удаляет первый встреченный элемент obj из очереди. Если удаление произшло, то возвращает true, иначе возвращает false  
> boolean removeLastOccurrence(Object obj): удаляет последний встреченный элемент obj из очереди. Если удаление произшло, то возвращает true, иначе возвращает false  
>```
>
>Таким образом, наличие методов *pop* и *push* позволяет классам, реализующим этот элемент, действовать в качестве *стека*. В тоже время имеющийся функционал также позволяет создавать *двунаправленные очереди*, что делает классы, применяющие данный интерфейс, довольно гибкими.
>
></details>
>
>**Класс ArrayDeque**
>
>Класс *ArrayDeque<E>* - представляет обобщенную двунаправленную очередь, наследуя функционал от класса AbstractCollection и применяя интерфейс Deque.
>
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

<details><summary>Класс LinkedList</summary>

>Представляет структуру данных в виде *связанного списка*. Он наследуется от класса AbstractSequentialList и реализует интерфейсы *List*, *Dequeue* и *Queue*. То есть он соединяет функциональность работы со *списком* и фукциональность *очереди*.
>
>Класс LinkedList имеет следующие конструкторы:
>```java
>LinkedList(): создает пустой список
>LinkedList(Collection<? extends E> col): создает список, в который добавляет все элементы коллекции col
>```
>*LinkedList* содержит все методы, которые определены в интерфейсах List, Queue, Deque вот некторые из них:
>```  
> addFirst() / offerFirst(): добавляет элемент в начало списка  
> addLast() / offerLast(): добавляет элемент в конец списка  
> removeFirst() / pollFirst(): удаляет первый элемент из начала списка  
> removeLast() / pollLast(): удаляет последний элемент из конца списка  
> getFirst() / peekFirst(): получает первый элемент  
> getLast() / peekLast(): получает последний элемент  
>```
>
>Примемр связанного списка LinkedList:
>
>[LinkedListDemo - Пример использования класса LinkedList и его методов](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceList/LinkedListDemo.java "Посмотреть пример Java")  
</details>

<details><summary>Интерфейс Set и класс HashSet</summary>

>**Интерфейс Set**
>
>Расширяет интерфейс *Collection* и представляет набор уникальных элементов, не допуская дублирования. *Set* не добавляет новых методов, а только вносит изменения в унаследованные методы. Например, метод add() добавляет элемент в коллекцию и возвращает true, если в коллекции не было такого элемента.
>
>**Обобщенный класс HashSet**
>
>Представляет хеш-таблицу. Он наследует свой функционал от класса *AbstractSet* и реализует интерфейс *Set*.
>Хеш-таблица представляет такую структуру данных, в которой все объекты имеют уникальный ключ или хеш-код. Данный ключ позволяет уникально идентифицировать объект в таблице.
>
>Для создания объекта HashSet можно воспользоваться одним из следующих конструкторов:  
>```java
>HashSet(): создает пустой список
>HashSet(Collection<? extends E> col): создает хеш-таблицу, в которую добавляет все элементы коллекции col
>HashSet(int capacity): параметр capacity указывает начальную емкость таблицы, которая по умолчанию равна 16
>HashSet(int capacity, float koef): параметр koef или коэффициент заполнения, значение которого должно быть в пределах от 0.0 до 1.0, 
>```  
>Коэффициент заполнения указывает, насколько должна быть заполнена емкость объектами прежде чем произойдет ее расширение. Например, коэффициент 0.75 указывает, что при заполнении емкости на 3/4 произойдет ее расширение.
>
>Класс HashSet реализует те методы, которые объявлены в родительских классах и применяемых интерфейсах:
>
>[HashSetDemo - Пример использования класса HashSet](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceSet/HashSetDemo.java "Посмотреть пример Java")
</details>

<details><summary>Интерфейсы SortedSet, NavigableSet и класс TreeSet</summary>

>**Интерфейс SortedSet**
>
>Предназначен для создания коллекций, где элементы хранятся в отсортированном (по возрастанию) виде. *SortedSet* расширяет нитерфейс *Set*, поэтому хранит только уникальные значения.
>
>*SortedSet* предоставляет следующие методы:
>```  
> E first(): возвращает первый элемент набора  
> E last(): возвращает последний элемент набора  
> SortedSet<E> headSet(E end): возвращает объект SortedSet, который содержит все элементы первичного набора до элемента end  
> SortedSet<E> subSet(E start, E end): возвращает объект SortedSet, который содержит все элементы первичного набора между элементами start и end  
> SortedSet<E> tailSet(E start): возвращает объект SortedSet, который содержит все элементы первичного набора, начиная с элемента start  
>```
>
>**Интерфейс NavigableSet**
>
>Расширяет интерфейс *SortedSet* и позволяет извлекать элементы на основании их значений.
> 
>*NavigableSet* определяет следующие методы:
>```  
> E ceiling(E obj): ищет в наборе наименьший элемент e, который больше obj (e >=obj). Если такой элемент найден, то он возвращается в качестве результата. Иначе возвращается null.  
> E floor(E obj): ищет в наборе наибольший элемент e, который меньше элемента obj (e <=obj). Если такой элемент найден, то он возвращается в качестве результата. Иначе возвращается null.  
> E higher(E obj): ищет в наборе наименьший элемент e, который больше элемента obj (e >obj). Если такой элемент найден, то он возвращается в качестве результата. Иначе возвращается null.  
> E lower(E obj): ищет в наборе наибольший элемент e, который меньше элемента obj (e <obj). Если такой элемент найден, то он возвращается в качестве результата. Иначе возвращается null.  
> E pollFirst(): возвращает первый элемент и удаляет его из набора  
> E pollLast(): возвращает последний элемент и удаляет его из набора  
> NavigableSet<E> descendingSet(): возвращает объект NavigableSet, который содержит все элементы первичного набора NavigableSet в обратном порядке  
> NavigableSet<E> headSet(E upperBound, boolean incl): возвращает объект NavigableSet, который содержит все элементы первичного набора NavigableSet до upperBound. Параметр incl при значении true, позволяет включить в выходной набор элемент upperBound  
> NavigableSet<E> tailSet(E lowerBound, boolean incl): возвращает объект NavigableSet, который содержит все элементы первичного набора NavigableSet, начиная с lowerBound. Параметр incl при значении true, позволяет включить в выходной набор элемент lowerBound  
> NavigableSet<E> subSet(E lowerBound, boolean lowerIncl, E upperBound, boolean highIncl): возвращает объект NavigableSet, который содержит все элементы первичного набора NavigableSet от lowerBound до upperBound.
>```
>
>**Обобщенный класс TreeSet<E>**
>
>Представляет структуру данных в виде дерева, в котором все объекты хранятся в отсортированном виде по возрастанию. *TreeSet* является наследником класса *AbstractSet* и реализует интерфейс *NavigableSet*, а следовательно, и интерфейс *SortedSet*.
>
>В классе *TreeSet* определены следующие конструкторы:  
>```java
>TreeSet(): создает пустое дерево  
>TreeSet(Collection<? extends E> col): создает дерево, в которое добавляет все элементы коллекции col  
>TreeSet(SortedSet <E> set): создает дерево, в которое добавляет все элементы сортированного набора set 
>TreeSet(Comparator<? super E> comparator): создает пустое дерево, где все добавляемые элементы впоследствии будут отсортированы компаратором  
>```
>*TreeSet* поддерживает все стандартные методы для вставки (при вставке объекты сразу же сортируются по возрастанию) и удаления элементов.
>  
>[TreeSetDemo - Пример использования класса TreeSet](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceSet/TreeSetDemo.java "Посмотреть пример Java")
</details>

<details><summary>Интерфейсы Comparable и Comparator + Сортировка</summary>

>
>**Интерфейс Comparable**
>
>Служит для сравнения и сортировки *Объектов*.
>Он содержит один единственный метод *int compareTo(E item)*, который сравнивает текущий объект с объектом, переданным в качестве параметра. Если этот метод возвращает отрицательное число, то текущий объект будет располагаться перед тем, который передается через параметр. Если метод вернет положительное число, то, наоборот, после второго объекта. Если метод возвратит ноль, значит, оба объекта равны.
>  
>[ComparableDemo - Пример типизации класса TreeSet объектом типа Person](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceComparable/ComparableDemo.java "Посмотреть пример Java")
>
>**Интерфейс Comparator**
>
>Применяется, если вдруг не реализован в своем классе , либо необходимо переопределить существующую функциональность интерфейса *Comparable*.  
>Он содержит ряд методов, ключевым из которых является метод compare():  
>```java
>public interface Comparator<E> {
>    int compare(T a, T b);
>    ... остальные методы
>}
>```  
>Метод *compare* также возвращает числовое значение. Если оно отрицательное, то объект a предшествует объекту b, иначе - наоборот, если метод возвращает ноль, то объекты равны. Для применения интерфейса нам вначале надо создать *класс компаратора*, который реализует этот интерфейс:
>  
>[ComparatorDemo - Пример использования класса компаратор для создания объекта TreeSet](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceComparator/ComparatorDemo.java "Посмотреть пример Java")
>
>**Сортировка по нескольким критериям**
>
>Начиная с JDK 8 в механизм работы компараторов были внесены некоторые дополнения. В частности, теперь мы можем применять сразу несколько компараторов по принципу приоритета.
>
>Интерфейс компаратора определяет специальный метод по умолчанию *thenComparing*, который позволяет использовать цепочки компараторов для сортировки набора. Например, нам надо отсортировать пользователей по имени и по возрасту:
>
>[ComparatorSortDemo - Пример использования цепочки компараторов для сортировки набора](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceComparator/ComparatorSortDemo.java "Посмотреть пример Java")
</details>

<details><summary>Интерфейс Map и класс HashMap</summary>

>**Интерфейс Map<K, V>**
>
>Представляет отображение, где каждый элемент представляет пару "ключ-значение". При этом все ключи уникальные в рамках объекта Map.
>Он НЕ расширяет интерфейс *Collection*.
>
>Среди методов интерфейса Map можно выделить следующие:
>```  
> void clear(): очищает коллекцию  
> boolean containsKey(Object k): возвращает true, если коллекция содержит ключ k  
> boolean containsValue(Object v): возвращает true, если коллекция содержит значение v  
> Set<Map.Entry<K, V>> entrySet(): возвращает набор элементов коллекции. Все элементы представляют объект Map.Entry  
> boolean equals(Object obj): возвращает true, если коллекция идентична коллекции, передаваемой через параметр obj  
> boolean isEmpty: возвращает true, если коллекция пуста  
> V get(Object k): возвращает значение объекта, ключ которого равен k. Если такого элемента не окажется, то возвращается значение null  
> V getOrDefault(Object k, V defaultValue): возвращает значение объекта, ключ которого равен k. Если такого элемента не окажется, то возвращается значение defaultVlue  
> V put(K k, V v): помещает в коллекцию новый объект с ключом k и значением v. Если в коллекции уже есть объект с подобным ключом, то он перезаписывается. После добавления возвращает предыдущее значение для ключа k, если он уже был в коллекции. Если же ключа еще не было в коллекции, то возвращается значение null  
> V putIfAbsent(K k, V v): помещает в коллекцию новый объект с ключом k и значением v, если в коллекции еще нет элемента с подобным ключом.  
> Set<K> keySet(): возвращает набор всех ключей отображения  
> Collection<V> values(): возвращает набор всех значений отображения  
> void putAll(Map<? extends K, ? extends V> map): добавляет в коллекцию все объекты из отображения map  
> V remove(Object k): удаляет объект с ключом k  
> int size(): возвращает количество элементов коллекции
>```
>
>Чтобы положить объект в коллекцию, используется метод *put*, а чтобы получить по ключу - метод *get*. Реализация интерфейса *Map* также позволяет получить наборы как ключей, так и значений. Метод *entrySet()* возвращает набор всех элементов в виде объектов *Map.Entry<K, V>*.
>
>**Обобщенный интерфейс Map.Entry<K, V>**
>
>Представляет объект с ключом типа K и значением типа V и определяет следующие методы:
>```
>boolean equals(Object obj): возвращает true, если объект obj, представляющий интерфейс Map.Entry, идентичен текущему  
>K getKey(): возвращает ключ объекта отображения  
>V getValue(): возвращает значение объекта отображения  
>V setValue(V v): устанавливает для текущего объекта значение v  
>int hashCode(): возвращает хеш-код данного объекта
>```  
>
>**Класс отображений HashMap** 
>
>Базовым классом для всех отображений является абстрактный класс *AbstractMap*, который реализует большую часть методов интерфейса *Map*. Наиболее распространенным классом отображений является *HashMap*, который реализует интерфейс *Map* и наследуется от класса *AbstractMap*.
>
>[HashMapDemo - Пример использования класса HashMap](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceMap/HashMapDemo.java "Посмотреть пример Java")  
>
</details>


<details><summary>Интерфейсы SortedMap и NavigableMap. Класс TreeMap</summary>

>**Интерфейс SortedMap**
>
>Расширяет *Map* и создает отображение, в котором все элементы *отсортированы* в порядке возрастания их ключей. 
>
>*SortedMap* добавляет ряд методов:
>```
>K firstKey(): возвращает ключ первого элемента отображения  
>K lastKey(): возвращает ключ последнего элемента отображения  
>SortedMap<K, V> headMap(K end): возвращает отображение SortedMap, которые содержит все элементы оригинального SortedMap вплоть до элемента с ключом end  
>SortedMap<K, V> tailMap(K start): возвращает отображение SortedMap, которые содержит все элементы оригинального SortedMap, начиная с элемента с ключом start  
>SortedMap<K, V> subMap(K start, K end): возвращает отображение SortedMap, которые содержит все элементы оригинального SortedMap вплоть от элемента с ключом start до элемента с ключом end  
>```
>
>**Интерфейс NavigableMap**
>
>Расширяет интерфейс *SortedMap* и обеспечивает возможность получения элементов отображения относительно других элементов. 
>
>Основные методы:
>```
>Map.Entry<K, V> ceilingEntry(K obj): возвращает элемент с наименьшим ключом k, который больше или равен ключу obj (k >=obj). Если такого ключа нет, то возвращается null.
>Map.Entry<K, V> floorEntry(K obj): возвращает элемент с наибольшим ключом k, который меньше или равен ключу obj (k <=obj). Если такого ключа нет, то возвращается null.
>Map.Entry<K, V> higherEntry(): возвращает элемент с наименьшим ключом k, который больше ключа obj (k >obj). Если такого ключа нет, то возвращается null.
>Map.Entry<K, V> lowerEntry(): возвращает элемент с наибольшим ключом k, который меньше ключа obj (k <obj). Если такого ключа нет, то возвращается null.
>Map.Entry<K, V> firstEntry(): возвращает первый элемент отображения
>Map.Entry<K, V> lastEntry(): возвращает последний элемент отображения
>Map.Entry<K, V> pollFirstEntry(): возвращает и одновременно удаляет первый элемент из отображения
>Map.Entry<K, V> pollLastEntry(): возвращает и одновременно удаляет последний элемент из отображения
>K ceilingKey(K obj): возвращает наименьший ключ k, который больше или равен ключу obj (k >=obj). Если такого ключа нет, то возвращается null.
>K floorKey(K obj): возвращает наибольший ключ k, который меньше или равен ключу obj (k <=obj). Если такого ключа нет, то возвращается null.
>K lowerKey(K obj): возвращает наибольший ключ k, который меньше ключа obj (k <obj). Если такого ключа нет, то возвращается null.
>K higherKey(K obj): возвращает наименьший ключ k, который больше ключа obj (k >obj). Если такого ключа нет, то возвращается null.
>NavigableSet<K> descendingKeySet(): возвращает объект NavigableSet, который содержит все ключи отображения в обратном порядке
>NavigableMap<K, V> descendingMap(): возвращает отображение NavigableMap, которое содержит все элементы в обратном порядке
>NavigableSet<K> navigableKeySet(): возвращает объект NavigableSet, который содержит все ключи отображения
>NavigableMap<K, V> headMap(K upperBound, boolean incl): возвращает отображение NavigableMap, которое содержит все элементы оригинального NavigableMap вплоть от элемента с ключом upperBound. Параметр incl при значении true указывает, что элемент с ключом upperBound также включается в выходной набор.
>NavigableMap<K, V> tailMap(K lowerBound, boolean incl): возвращает отображение NavigableMap, которое содержит все элементы оригинального NavigableMap, начиная с элемента с ключом lowerBound. Параметр incl при значении true указывает, что элемент с ключом lowerBound также включается в выходной набор.
>NavigableMap<K, V> subMap(K lowerBound, boolean lowIncl, K upperBound, boolean highIncl): возвращает отображение NavigableMap, которое содержит все элементы оригинального NavigableMap от элемента с ключом lowerBound до элемента с ключом upperBound. Параметры lowIncl и highIncl при значении true включают в выходной набор элементы с ключами lowerBound и upperBound соответственно.
>```
>
>**Класс TreeMap<K, V>**
>
>Представляет отображение в виде дерева. Он наследуется от класса *AbstractMap* и реализует интерфейс *NavigableMap*, соответсвенно, также и интерфейс *SortedMap*. Поэтому в отличие от коллекции *HashMap* в *TreeMap* все объекты *автоматически сортируются по возрастанию их ключей*.
>
>Класс *TreeMap* имеет следующие конструкторы:
>```
>TreeMap(): создает пустое отображение в виде дерева
>TreeMap(Map<? extends K, ? extends V> map): создает дерево, в которое добавляет все элементы из отображения map
>TreeMap(SortedMap<K, ? extends V> smap): создает дерево, в которое добавляет все элементы из отображения smap
>TreeMap(Comparator<? super K> comparator): создает пустое дерево, где все добавляемые элементы впоследствии будут отсортированы компаратором.
>```
>[TreeMapDemo - Пример использования класса TreeMap](https://github.com/aykononov/JavaCollections/blob/master/src/InterfaceMap/TreeMapDemo.java "Посмотреть пример Java")
>
>Кроме методов интерфейса *Map* класс *TreeMap* реализует методы интерфейса *NavigableMap*. Например, можно получить все объекты *до* или *после* определенного ключа с помощью методов *headMap* и *tailMap*. Также можно получить *первый* и *последний* элементы и провести ряд дополнительных манипуляций с объектами.
>
>*Для того чтобы получить ключ по значению придется использовать ПЕРЕБОР, так как такого метода НЕТ.* 
>
</details>

</small>