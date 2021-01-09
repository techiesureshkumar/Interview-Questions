1) What is Java Collections Framework? List out some benefits of Collections framework?

* Collections are used in every programming language.
* Few classes for collections: Vector, Stack, Hashtable, Array. 
* Collections Framework that group all the collections interfaces, implementations and algorithms.
* Java Collections have come through a long way with the usage of Generics and Concurrent Collection classes for thread-safe operations. 
* It also includes blocking interfaces and their implementations in java concurrent package.

Benefits
--------
* Reduced development effort by using core collection classes rather than implementing our own collection classes.
* Code quality is enhanced with the use of well tested collections framework classes.
* Reduced effort for code maintenance by using collection classes shipped with JDK.
* Reusability and Interoperability

2) What are the main differences between array and collection?

Array and Collection are somewhat similar regarding storing the references of objects and manipulating the data, but they differ in many ways. The main differences between the array and Collection are defined below:

* Arrays are always of fixed size, i.e., a user can not increase or decrease the length of the array according to their requirement or at runtime, but In Collection, size can be changed dynamically as per need.
* Arrays can only store homogeneous or similar type objects, but in Collection, heterogeneous objects can be stored.
* Arrays cannot provide the ?ready-made? methods for user requirements as sorting, searching, etc. but Collection includes readymade methods to use.

3) What is the benefit of Generics in Collections Framework?

Java 1.5 came with Generics and all collection interfaces and implementations use it heavily. Generics allow us to provide the type of Object that a collection can contain, so if you try to add any element of other type it throws compile time error.
This avoids ClassCastException at Runtime because you will get the error at compilation. Also Generics make code clean since we don’t need to use casting and instanceof operator.

4) What are the basic interfaces of Java Collections Framework?

* Collection is the root of the collection hierarchy. A collection represents a group of objects known as its elements. The Java platform doesn’t provide any direct implementations of this interface.

* Set is a collection that cannot contain duplicate elements. This interface models the mathematical set abstraction and is used to represent sets, such as the deck of cards.

* List is an ordered collection and can contain duplicate elements. You can access any element from its index. The list is more like an array with dynamic length.

* A Map is an object that maps keys to values. A map cannot contain duplicate keys: Each key can map to at most one value.

* Some other interfaces are Queue, Dequeue, Iterator, SortedSet, SortedMap and ListIterator.

5) Why Collection doesn’t extend Cloneable and Serializable interfaces?

Collection interface specifies group of Objects known as elements. How the elements are maintained is left up to the concrete implementations of Collection. For example, some Collection implementations like List allow duplicate elements whereas other implementations like Set don’t.
A lot of the Collection implementations have a public clone method. However, it doesn’t make sense to include it in all implementations of Collection. This is because Collection is an abstract representation. What matters is the implementation.
The semantics and the implications of either cloning or serializing come into play when dealing with the actual implementation; so concrete implementation should decide how it should be cloned or serialized, or even if it can be cloned or serialized.
So mandating cloning and serialization in all implementations is less flexible and more restrictive. The specific implementation should decide as to whether it can be cloned or serialized.

6)Why Map interface doesn’t extend Collection interface?

Although Map interface and its implementations are part of the Collections Framework, Map is not collections and collections are not Map. Hence it doesn’t make sense for Map to extend Collection or vice versa.
If Map extends Collection interface, then where are the elements? The map contains key-value pairs and it provides methods to retrieve the list of Keys or values as Collection but it doesn’t fit into the “group of elements” paradigm.

7) What is an Iterator?

The Iterator interface provides methods to iterate over any Collection. We can get iterator instance from a Collection using iterator() method. Iterator takes the place of Enumeration in the Java Collections Framework. Iterators allow the caller to remove elements from the underlying collection during the iteration. Java Collection iterator provides a generic way for traversal through the elements of a collection and implements Iterator Design Pattern.

8) What is difference between Enumeration and Iterator interface?

Enumeration is twice as fast as Iterator and uses very little memory. Enumeration is very basic and fits basic needs. But the Iterator is much safer as compared to Enumeration because it always denies other threads to modify the collection object which is being iterated by it.
Iterator takes the place of Enumeration in the Java Collections Framework. Iterators allow the caller to remove elements from the underlying collection that is not possible with Enumeration. Iterator method names have been improved to make its functionality clear.

9) Why there is not method like Iterator.add() to add elements to the collection?

The semantics are unclear, given that the contract for Iterator makes no guarantees about the order of iteration. Note, however, that ListIterator does provide an add operation, as it does guarantee the order of the iteration.

10) Why Iterator don’t have a method to get next element directly without moving the cursor?

It can be implemented on top of current Iterator interface but since its use will be rare, it doesn’t make sense to include it in the interface that everyone has to implement.

11) What is different between Iterator and ListIterator?

We can use Iterator to traverse Set and List collections whereas ListIterator can be used with Lists only.
Iterator can traverse in forward direction only whereas ListIterator can be used to traverse in both the directions.
ListIterator inherits from Iterator interface and comes with extra functionalities like adding an element, replacing an element, getting index position for previous and next elements.

12) What are different ways to iterate over a list?

We can iterate over a list in two different ways – using iterator and using for-each loop.

List<String> strList = new ArrayList<>();

//using for-each loop
for(String obj : strList){
    System.out.println(obj);
}

//using iterator
Iterator<String> it = strList.iterator();
while(it.hasNext()){
    String obj = it.next();
    System.out.println(obj);
}
Using iterator is more thread-safe because it makes sure that if underlying list elements are modified, it will throw ConcurrentModificationException.
    
13) What do you understand by iterator fail-fast property?

Iterator fail-fast property checks for any modification in the structure of the underlying collection everytime we try to get the next element. If there are any modifications found, it throws ConcurrentModificationException. All the implementations of Iterator in Collection classes are fail-fast by design except the concurrent collection classes like ConcurrentHashMap and CopyOnWriteArrayList.

14) What is difference between fail-fast and fail-safe?

Iterator fail-safe property work with the clone of underlying collection, hence it’s not affected by any modification in the collection. By design, all the collection classes in java.util package are fail-fast whereas collection classes in java.util.concurrent are fail-safe.
Fail-fast iterators throw ConcurrentModificationException whereas fail-safe iterator never throws ConcurrentModificationException.
Check this post for CopyOnWriteArrayList Example.

15) CopyOnWriteArrayList in Java?

Sometimes we want to add or remove elements from the list if we find some specific element, in that case we should use concurrent collection class – CopyOnWriteArrayList. This is a thread-safe variant of java.util.ArrayList in which all mutative operations (add, set, and so on) are implemented by making a fresh copy of the underlying array.

CopyOnWriteArrayList introduces extra overload to the processing but it’s very effective when number of modifications are minimal compared to number of traversal operations.

If we change the implementation to CopyOnWriteArrayList, then we don’t get any exception and below is the output produced.

1) list is:[1, 2, 3, 4, 5]
2) list is:[1, 2, 3, 4, 5]
3) list is:[1, 2, 3, 4]
4) list is:[1, 2, 3, 4, 3 found]
5) list is:[1, 4, 3, 4, 3 found]
Notice that it allows the modification of list, but it doesn’t change the iterator and we get same elements as it was on original list.

16) How to avoid ConcurrentModificationException while iterating a collection?

We can use concurrent collection classes to avoid ConcurrentModificationException while iterating over a collection, for example CopyOnWriteArrayList instead of ArrayList.
Check this post for ConcurrentHashMap Example.

17) Why there are no concrete implementations of Iterator interface?

Iterator interface declare methods for iterating a collection but its implementation is responsibility of the Collection implementation classes. Every collection class that returns an iterator for traversing has its own Iterator implementation nested class.
This allows collection classes to chose whether iterator is fail-fast or fail-safe. 
For example ArrayList iterator is fail-fast whereas CopyOnWriteArrayList iterator is fail-safe.

18) What is UnsupportedOperationException?

UnsupportedOperationException is the exception used to indicate that the operation is not supported. It’s used extensively in JDK classes, in collections framework java.util.Collections.UnmodifiableCollection throws this exception for all add and remove operations.

19) How HashMap works in Java? -- need modification

HashMap stores key-value pair in Map.Entry static nested class implementation. HashMap works on hashing algorithm and uses hashCode() and equals() method in put and get methods.

When we call put method by passing key-value pair, HashMap uses Key hashCode() with hashing to find out the index to store the key-value pair. The Entry is stored in the LinkedList, so if there is an already existing entry, it uses equals() method to check if the passed key already exists, if yes it overwrites the value else it creates a new entry and stores this key-value Entry.

When we call get method by passing Key, again it uses the hashCode() to find the index in the array and then use equals() method to find the correct Entry and return its value. The below image will explain these detail clearly.

The other important things to know about HashMap are capacity, load factor, threshold resizing. HashMap initial default capacity is 16 and load factor is 0.75. The threshold is capacity multiplied by load factor and whenever we try to add an entry if map size is greater than the threshold, HashMap rehashes the contents of the map into a new array with a larger capacity. The capacity is always the power of 2, so if you know that you need to store a large number of key-value pairs, for example in caching data from the database, it’s a good idea to initialize the HashMap with correct capacity and load factor.

20) What is the importance of hashCode() and equals() methods? -- Need. modification

HashMap uses the Key object hashCode() and equals() method to determine the index to put the key-value pair. These methods are also used when we try to get value from HashMap. If these methods are not implemented correctly, two different Key’s might produce the same hashCode() and equals() output and in that case, rather than storing it at a different location, HashMap will consider the same and overwrite them.

Similarly all the collection classes that doesn’t store duplicate data use hashCode() and equals() to find duplicates, so it’s very important to implement them correctly. The implementation of equals() and hashCode() should follow these rules.

If o1.equals(o2), then o1.hashCode() == o2.hashCode()should always be true.
If o1.hashCode() == o2.hashCode is true, it doesn’t mean that o1.equals(o2) will be true.

21) Can we use any class as Map key? --Need Modification
We can use any class as Map Key, however following points should be considered before using them.

If the class overrides equals() method, it should also override hashCode() method.
The class should follow the rules associated with equals() and hashCode() for all instances. Please refer earlier question for these rules.
If a class field is not used in equals(), you should not use it in hashCode() method.
Best practice for user defined key class is to make it immutable, so that hashCode() value can be cached for fast performance. Also immutable classes make sure that hashCode() and equals() will not change in future that will solve any issue with mutability.
For example, let’s say I have a class MyKey that I am using for the HashMap key.

//MyKey name argument passed is used for equals() and hashCode()
MyKey key = new MyKey("Pankaj"); //assume hashCode=1234
myHashMap.put(key, "Value");

// Below code will change the key hashCode() and equals()
// but its location is not changed.
key.setName("Amit"); //assume new hashCode=7890

//below will return null because HashMap will try to look for key
//in the same index as it was stored but since the key is mutated, 
//there will be no match and it will return null.
myHashMap.get(new MyKey("Pankaj")); 
This is the reason why String and Integer are mostly used as HashMap keys.

22) What are different Collection views provided by Map interface? --Need Modification

Map interface provides three collection views:

Set<K> keySet(): Returns a Set view of the keys contained in this map. The set is backed by the map, so changes to the map are reflected in the set, and vice-versa. If the map is modified while an iteration over the set is in progress (except through the iterator’s remove operation), the results of the iteration are undefined. The set supports element removal, which removes the corresponding mapping from the map, via the Iterator remove, Set.remove, removeAll, retainAll, and clear operations. It does not support the add or addAll operations.
    
Collection<V> values(): Returns a Collection view of the values contained in this map. The collection is backed by the map, so changes to the map are reflected in the collection, and vice-versa. If the map is modified while an iteration over the collection is in progress (except through the iterator’s remove operation), the results of the iteration are undefined. The collection supports element removal, which removes the corresponding mapping from the map, via the Iterator remove, Collection.remove, removeAll, retainAll, and clear operations. It does not support the add or addAll operations.
    
Set<Map.Entry<K, V>> entrySet(): Returns a Set view of the mappings contained in this map. The set is backed by the map, so changes to the map are reflected in the set, and vice-versa. If the map is modified while an iteration over the set is in progress (except through the iterator’s remove operation, or the setValue operation on a map entry returned by the iterator) the results of the iteration are undefined. The set supports element removal, which removes the corresponding mapping from the map, via the Iterator remove, Set.remove, removeAll, retainAll, and clear operations. It does not support the add or addAll operations.

23) What is difference between HashMap and Hashtable?

HashMap and Hashtable both implements Map interface and looks similar, however, there is the following difference between HashMap and Hashtable.

HashMap allows null key and values whereas Hashtable doesn’t allow null key and values.
Hashtable is synchronized but HashMap is not synchronized. So HashMap is better for single threaded environment, Hashtable is suitable for multi-threaded environment.
LinkedHashMap was introduced in Java 1.4 as a subclass of HashMap, so incase you want iteration order, you can easily switch from HashMap to LinkedHashMap but that is not the case with Hashtable whose iteration order is unpredictable.
HashMap provides Set of keys to iterate and hence it’s fail-fast but Hashtable provides Enumeration of keys that doesn’t support this feature.
Hashtable is considered to be legacy class and if you are looking for modifications of Map while iterating, you should use ConcurrentHashMap.

24) How to decide between HashMap and TreeMap?

For inserting, deleting, and locating elements in a Map, the HashMap offers the best alternative. If, however, you need to traverse the keys in a sorted order, then TreeMap is your better alternative. Depending upon the size of your collection, it may be faster to add elements to a HashMap, then convert the map to a TreeMap for sorted key traversal.

25) What are similarities and difference between ArrayList and Vector?

ArrayList and Vector are similar classes in many ways.

Both are index based and backed up by an array internally.
Both maintains the order of insertion and we can get the elements in the order of insertion.
The iterator implementations of ArrayList and Vector both are fail-fast by design.
ArrayList and Vector both allows null values and random access to element using index number.

26) What are the differences between ArrayList and Vector?

Vector is synchronized whereas ArrayList is not synchronized. However if you are looking for modification of list while iterating, you should use CopyOnWriteArrayList.
ArrayList is faster than Vector because it doesn’t have any overhead because of synchronization.
ArrayList is more versatile because we can get synchronized list or read-only list from it easily using Collections utility class.

27) What is difference between Array and ArrayList? When will you use Array over ArrayList?

Arrays can contain primitive or Objects whereas ArrayList can contain only Objects.
Arrays are fixed-size whereas ArrayList size is dynamic.
Arrays don’t provide a lot of features like ArrayList, such as addAll, removeAll, iterator, etc.

Although ArrayList is the obvious choice when we work on the list, there are a few times when an array is good to use.

If the size of list is fixed and mostly used to store and traverse them.
For list of primitive data types, although Collections use autoboxing to reduce the coding effort but still it makes them slow when working on fixed size primitive data types.
If you are working on fixed multi-dimensional situation, using [][] is far more easier than List<List<>>

28) What is difference between ArrayList and LinkedList?

ArrayList and LinkedList both implement List interface but there are some differences between them.

ArrayList is an index based data structure backed by Array, so it provides random access to its elements with performance as O(1) but LinkedList stores data as list of nodes where every node is linked to its previous and next node. So even though there is a method to get the element using index, internally it traverse from start to reach at the index node and then return the element, so performance is O(n) that is slower than ArrayList.

Insertion, addition or removal of an element is faster in LinkedList compared to ArrayList because there is no concept of resizing array or updating index when element is added in middle.
LinkedList consumes more memory than ArrayList because every node in LinkedList stores reference of previous and next elements.

29) Which collection classes provide random access of its elements?

ArrayList, HashMap, TreeMap, Hashtable, and Vector classes provide random access to its elements.

30) What is EnumSet?

java.util.EnumSet is Set implementation to use with enum types. All of the elements in an enum set must come from a single enum type that is specified, explicitly or implicitly, when the set is created. EnumSet is not synchronized and null elements are not allowed. It also provides some useful methods like copyOf(Collection c), of(E first, E… rest) and complementOf(EnumSet s).

31) Which collection classes are thread-safe?

Vector, Hashtable, Properties and Stack are synchronized classes, so they are thread-safe and can be used in multi-threaded environment. Java 1.5 Concurrent API included some collection classes that allows modification of collection while iteration because they work on the clone of the collection, so they are safe to use in multi-threaded environment.

32) What are concurrent Collection Classes?

Java 1.5 Concurrent package (java.util.concurrent) contains thread-safe collection classes that allow collections to be modified while iterating. By design Iterator implementation in java.util packages are fail-fast and throws ConcurrentModificationException. But Iterator implementation in java.util.concurrent packages are fail-safe and we can modify the collection while iterating. Some of these classes are CopyOnWriteArrayList, ConcurrentHashMap, CopyOnWriteArraySet.

33) What is BlockingQueue? --Need Modification

java.util.concurrent.BlockingQueue is a Queue that supports operations that wait for the queue to become non-empty when retrieving and removing an element, and wait for space to become available in the queue when adding an element.

BlockingQueue interface is part of the java collections framework and it’s primarily used for implementing the producer-consumer problem. We don’t need to worry about waiting for the space to be available for producer or object to be available for consumers in BlockingQueue as it’s handled by implementation classes of BlockingQueue.

Java provides several BlockingQueue implementations such as ArrayBlockingQueue, LinkedBlockingQueue, PriorityBlockingQueue, SynchronousQueue, etc.

34) What is Queue and Stack, list their differences?

Both Queue and Stack are used to store data before processing them. java.util.Queue is an interface whose implementation classes are present in java concurrent package. Queue allows retrieval of element in First-In-First-Out (FIFO) order but it’s not always the case. There is also Deque interface that allows elements to be retrieved from both end of the queue.
The stack is similar to queue except that it allows elements to be retrieved in Last-In-First-Out (LIFO) order.
Stack is a class that extends Vector whereas Queue is an interface.

35) What is Collections Class? --Need Modification

java.util.Collections is a utility class consists exclusively of static methods that operate on or return collections. It contains polymorphic algorithms that operate on collections, “wrappers”, which return a new collection backed by a specified collection, and a few other odds and ends.

This class contains methods for collection framework algorithms, such as binary search, sorting, shuffling, reverse, etc.

36) Binary search, sorting, shuffling, reverse. How does this happen in Collections? --Need modification

37) What is Comparable and Comparator interface?

Java provides a Comparable interface which should be implemented by any custom class if we want to use Arrays or Collections sorting methods. The comparable interface has a compareTo(T obj) method which is used by sorting methods. We should override this method in such a way that it returns a negative integer, zero, or a positive integer if “this” object is less than, equal to, or greater than the object passed as an argument.

But, in most real-life scenarios, we want sorting based on different parameters. For example, as a CEO, I would like to sort the employees based on Salary, an HR would like to sort them based on age. This is the situation where we need to use Comparator interface because Comparable.compareTo(Object o) method implementation can sort based on one field only and we can’t choose the field on which we want to sort the Object.

Comparator interface compare(Object o1, Object o2) method need to be implemented that takes two Object argument, it should be implemented in such a way that it returns negative int if the first argument is less than the second one and returns zero if they are equal and positive int if the first argument is greater than the second one.

38) What is difference between Comparable and Comparator interface?

Comparable and Comparator interfaces are used to sort collection or array of objects.

Comparable interface is used to provide the natural sorting of objects and we can use it to provide sorting based on single logic.
Comparator interface is used to provide different algorithms for sorting and we can choose the comparator we want to use to sort the given collection of objects.

39) How can we sort a list of Objects?

If we need to sort an array of Objects, we can use Arrays.sort(). If we need to sort a list of objects, we can use Collections.sort(). Both these classes have overloaded sort() methods for natural sorting (using Comparable) or sorting based on criteria (using Comparator).
Collections internally uses Arrays sorting method, so both of them have same performance except that Collections take sometime to convert list to array.

40) While passing a Collection as argument to a function, how can we make sure the function will not be able to modify it?

We can create a read-only collection using Collections.unmodifiableCollection(Collection c) method before passing it as argument, this will make sure that any operation to change the collection will throw UnsupportedOperationException.

41) How can we create a synchronized collection from given collection?

We can use Collections.synchronizedCollection(Collection c) to get a synchronized (thread-safe) collection backed by the specified collection.

42) What are common algorithms implemented in Collections Framework?

Java Collections Framework provides algorithm implementations that are commonly used such as sorting and searching. Collections class contain these method implementations. Most of these algorithms work on List but some of them are applicable for all kinds of collections.
Some of them are sorting, searching, shuffling, min-max values.

43) What is Big-O notation? Give some examples?

The Big-O notation describes the performance of an algorithm in terms of the number of elements in a data structure. Since Collection classes are data structures, we usually tend to use Big-O notation to chose the collection implementation to use based on time, memory and performance.

Example 1: ArrayList get(index i) is a constant-time operation and doesn’t depend on the number of elements in the list. So its performance in Big-O notation is O(1).
Example 2: A linear search on array or list performance is O(n) because we need to search through entire list of elements to find the element.

44) What are best practices related to Java Collections Framework?

Chosing the right type of collection based on the need, for example if size is fixed, we might want to use Array over ArrayList. If we have to iterate over the Map in order of insertion, we need to use LinkedHashMap. If we don’t want duplicates, we should use Set.
Some collection classes allows to specify the initial capacity, so if we have an estimate of number of elements we will store, we can use it to avoid rehashing or resizing.
Write program in terms of interfaces not implementations, it allows us to change the implementation easily at later point of time.
Always use Generics for type-safety and avoid ClassCastException at runtime.
Use immutable classes provided by JDK as key in Map to avoid implementation of hashCode() and equals() for our custom class.
Use Collections utility class as much as possible for algorithms or to get read-only, synchronized or empty collections rather than writing own implementation. It will enhance code-reuse with greater stability and low maintainability.

45) What is Java Priority Queue?

PriorityQueue is an unbounded queue based on a priority heap and the elements are ordered in their natural order or we can provide Comparator for ordering at the time of creation. PriorityQueue doesn’t allow null values and we can’t add any object that doesn’t provide natural ordering or we don’t have any comparator for them for ordering. Java PriorityQueue is not thread-safe and provided O(log(n)) time for enqueing and dequeing operations. Check this post for java priority queue example.

For example, let’s say we have an application that generates stocks reports for daily trading session. This application processes a lot of data and takes time to process it. So customers are sending request to the application that is actually getting queued but we want to process premium customers first and standard customers after them. So in this case PriorityQueue implementation in java can be really helpful.

The head of the priority queue is the least element based on the natural ordering or comparator based ordering, if there are multiple objects with same ordering, then it can poll any one of them randomly. When we poll the queue, it returns the head object from the queue.

Java Priority Queue size is unbounded but we can specify the initial capacity at the time of it’s creation. When we add elements to the priority queue, it’s capacity grows automatically.

PriorityQueue is not thread safe, so java provides PriorityBlockingQueue class that implements the BlockingQueue interface to use in java multithreading environment.

Java Priority Queue implementation provides O(log(n)) time for enqueing and dequeing method.

Let’s see an example of java PriorityQueue for natural ordering as well as with Comparator.

https://www.journaldev.com/1642/java-priority-queue-priorityqueue-example

package com.journaldev.collections;

import java.util.Comparator;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.Random;

public class PriorityQueueExample {

	public static void main(String[] args) {
		
		//natural ordering example of priority queue
		Queue<Integer> integerPriorityQueue = new PriorityQueue<>(7);
		Random rand = new Random();
		for(int i=0;i<7;i++){
			integerPriorityQueue.add(new Integer(rand.nextInt(100)));
		}
		for(int i=0;i<7;i++){
			Integer in = integerPriorityQueue.poll();
			System.out.println("Processing Integer:"+in);
		}
		
		//PriorityQueue example with Comparator
		Queue<Customer> customerPriorityQueue = new PriorityQueue<>(7, idComparator);
		addDataToQueue(customerPriorityQueue);
		
		pollDataFromQueue(customerPriorityQueue);
		
	}
	
	//Comparator anonymous class implementation
	public static Comparator<Customer> idComparator = new Comparator<Customer>(){
		
		@Override
		public int compare(Customer c1, Customer c2) {
            return (int) (c1.getId() - c2.getId());
        }
	};

	//utility method to add random data to Queue
	private static void addDataToQueue(Queue<Customer> customerPriorityQueue) {
		Random rand = new Random();
		for(int i=0; i<7; i++){
			int id = rand.nextInt(100);
			customerPriorityQueue.add(new Customer(id, "Pankaj "+id));
		}
	}
	
	//utility method to poll data from queue
	private static void pollDataFromQueue(Queue<Customer> customerPriorityQueue) {
		while(true){
			Customer cust = customerPriorityQueue.poll();
			if(cust == null) break;
			System.out.println("Processing Customer with ID="+cust.getId());
		}
	}

}

Processing Integer:9
Processing Integer:16
Processing Integer:18
Processing Integer:25
Processing Integer:33
Processing Integer:75
Processing Integer:77
Processing Customer with ID=6
Processing Customer with ID=20
Processing Customer with ID=24
Processing Customer with ID=28
Processing Customer with ID=29
Processing Customer with ID=82
Processing Customer with ID=96
