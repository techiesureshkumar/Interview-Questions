1) What is Java Collections Framework? List out some benefits of Collections framework?

Collections are used in every programming language and initial java release contained few classes for collections: Vector, Stack, Hashtable, Array. 
Collections Framework that group all the collections interfaces, implementations and algorithms.
Java Collections have come through a long way with the usage of Generics and Concurrent Collection classes for thread-safe operations. It also includes blocking interfaces and their implementations in java concurrent package.

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
