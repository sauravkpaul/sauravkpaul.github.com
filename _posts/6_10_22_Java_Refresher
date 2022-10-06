---
layout: post
title:  Java All basic DS refresher
categories: [Data Structures, Java]
---

## Java refresher

The below Demo code include all basic DS and Collections framework in Java. Can take a glance to refresh the Java Syntax for DS problems. 

```Java
import java.util.*;

class Main {
	public static void main(String args[]) {
		
		// All Data Structures in java
		
		//Arrays
		int intArray[];    //declaring array
    intArray = new int[20];  // allocating memory to array
    //or       
    int[] intArr = new int[20]; // combining both statements in one
		int[] intArrays = new int[]{ 1,2,3 };
		for(int i =0; i < 3; i++ ) System.out.print(intArrays[i] + " ");
		System.out.println();
		//Strings in Java 
		
		String s1 = new String("example");
		System.out.println("String s1 = " + s1);
		//String Buffer
		StringBuffer sb = new StringBuffer("JavaStringBuilder");
		//String Builder
		StringBuilder str = new StringBuilder();
		str.append("SBString");
		System.out.println("built String " + str);
		
		//ArrayList

		List<Integer> test = new ArrayList<>();
		test.add(1);
		test.add(2);
		test.add(3);
		System.out.println(test);
		
		//LinkedList
    LinkedList<Integer> ll = new LinkedList<Integer>(); // Declaring the LinkedList
  
    // Appending new elements at
    // the end of the list
    for (int i = 1; i <= 5; i++)
        ll.add(i);
  
    System.out.println(ll);
  
    // Remove element at index 3
    ll.remove(3);
		
		//Queue
		Queue<Integer> Q = new LinkedList<>();
		Q.add(1);
		System.out.println(Q.poll());
		System.out.println(Q.size());
		
		
		//Priority Queue
		PriorityQueue<Integer> pq = new PriorityQueue<Integer>();
		pq.add(20);
		pq.add(10);
		pq.add(30);
		int top = pq.peek(); //get the top element
		while(!pq.isEmpty()) System.out.println("PQ: " + pq.poll()); //get and remove
		
		//Deque
		// Initializing an deque
    ArrayDeque<Integer> de_que = new ArrayDeque<Integer>(10);
  
    // add() method to insert
    de_que.add(10);
    de_que.addFirst(20);
    de_que.addLast(30);
    System.out.println("DEQUE: " + de_que);
    de_que.clear();
		
		//Stack
		Stack<String> stack = new Stack<String>();
    stack.push("Stack");
    stack.push("DS");
    stack.push("In");
    stack.push("Java");
  
    // Iterator for the stack
    Iterator<String> sitr = stack.iterator();
  
    // Printing the stack
    while (sitr.hasNext()) {
        System.out.print(sitr.next() + " ");
    }
    System.out.println(stack.pop());
  
  
    //Set 
		System.out.println("SETs");
		HashSet<String> hs = new HashSet<String>();
    hs.add("Set");
    hs.add("Collections");
    hs.add("Java");
		Iterator<String> itr = hs.iterator();
    while (itr.hasNext()) {
        System.out.println(itr.next());
    }
		System.out.println("HasshSet contains Java? " + hs.contains("Java"));
		
		/*
		LinkedHashSet: A LinkedHashSet is very similar to a HashSet. 
		The difference is that this uses a doubly linked list to store the data \
		and retains the ordering of the elements. 
		Let us understand the LinkedHashSet with an example: 
		*/
		LinkedHashSet<int[]> lhs = new LinkedHashSet<int[]>();
    lhs.add(new int[]{0, 1});
    lhs.add(new int[]{1, 2});
		lhs.add(new int[]{3, 1});
  
     // Traversing elements
    Iterator<int[]> aitr = lhs.iterator();
		System.out.println("LinkedHashSet");
    while (aitr.hasNext()) {
        System.out.println(aitr.next()[0]);
    }
		
		//TreeSet
		TreeSet<String> ts = new TreeSet<String>();
    ts.add("Geeks");
    ts.add("For");
    ts.add("Geeks");
    System.out.println("TreeSet " + ts);
		
		// Map
		HashMap<Integer, String> hm = new HashMap<Integer, String>();
    hm.put(1, "HashMaps");
    hm.put(2, "In");
    hm.put(3, "Java");
		if (hm.containsKey(3))
		    System.out.println("Map: Value for 1 is " + hm.get(3));
		
		// Traversing through the HashMap
    for (Map.Entry<Integer, String> e : hm.entrySet())
        System.out.println(e.getKey() + " " + e.getValue());
			
		//Hash Table
		Hashtable<Integer, String> ht = new Hashtable<>();
  
    // Inserting the Elements using put method
    ht.put(1, "Geeks");
    ht.put(2, "Geeks");
    ht.put(3, "Geeks");
          
    // print initial map to the console
    System.out.println("Initial Map " + ht);
          
    // Update the value at key 2
    ht.put(2, "For");
		
		if (ht.containsKey(2)) System.out.println("HT for key 2 " + ht.get(2));
	}
}
```
