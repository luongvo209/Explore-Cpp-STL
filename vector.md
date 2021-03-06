# Introduction to Vectors in C++  

![](images/vector.png)  

**Acknowledgement:** *Everything written below is from my own experience in college and after reading various materials. I am neither a professional nor expert, but a student who has great passion for the language. Anyone can open a discussion in the issue section, or a pull request in case something should be modified or added. If you consider my work valuable, a [donation](#donation) is much appreciated.*


## Table of Contents:

1. [What the heck is Vectors in C++](#what-the-heck-is-vectors-in-c-)
2. [Isnt vector a data type?](#isnt-vector-a-data-type-)
3. [How do we use vectors ?](#how-do-we-use-vectors-)
4. [Operations on vectors](#operations-on-vectors)
  * [Input](#input)
  * [Assign](#assign)
  * [Insert](#insert)
  * [Comparison Operators](#comparison-operators)
  * [Size](#size)
  * [Output](#output)
  * [Erase](#erase)
  * [Clear](#clear)
  * [Resize](#resize)
  * [Other Good Stuffs](#other-good-stuffs)
5. [Iterators](#iterators)



## What the heck is Vectors in C++ ? 

In any kinds of programming languages, we can store various data of the same type in an array. However, basic types of array never serve what we need sufficiently. It is either hard to operate since we are coding from the ground up or impossible to implement due to some restrictions (i.e: hardware, performance....). Smart people, therefore came up with dynamically allocated array ( read more [here](https://github.com/tuvttran/curated-guides/blob/master/PointerC%2B%2B.md#pointers-and-dynamic-memory) ) but still, find their codes not relevant enough sometimes and the process of utilizing dynamically allocated array prone to errors, hard to maintain....

Now, they want something **standardized**, **easy to use** yet **perform efficiently** ( little or no compromise here!).

And then born the **Vector** .

To sum up, vectors are like dynamic array, but much much more powerful and easier to use.


## Isn't vector a data type ?

Wait, but I can't `vector + name_of_variable`! That's not a data type?

No. Vector is built in C++ Standard Template Library ( [C++ STL](https://en.wikipedia.org/wiki/Standard_Template_Library) ).

In short, C++ STL is a powerful library of templates which provides general-purpose templatized classes and functions that implement many popular and commonly used algorithms and data structures like vectors, lists, queues, and stacks (more on these later).

So yeah, now you understand that vector is **standardized** ! And it's much more than a data type.


## How do we use vectors ?

That's a good question! Vectors are meant to be **easy to use** so no worry here.

* Firstly, you need to call the vector from the header file.

```c++
#include <vector>
```
and remeber the 
```c++
using namespace std;
```
because vetor belongs to Standard Template Library.

* Secondly, let's consider the syntax of initializing a vector.

```c++
vector<int> A;   //default constructor, construct vector A with no elements inside.
```
Easily guess that one out , the code follows this rule : vector<data_type> vector_name.

Vector doesnt require you to add the size of the data (it's dynamic).But if you'd like to, -> **vector<data_type> vector_name (number_of_elements)**.

Oh, and if you'd like the intial vector to store something, you are welcome to add in -> **vector<data_type> vector_name  (number_of_elements , something_to_fulfill)**

For example :

```c++
vector<int> A (10, 5);
```

will make a vector of ten elements, each element's value is 5. Now let's consider another example :

```c++
vector<int> A (10,5);
vector<int> B (A);
```

**Now this one will copy the whole vector A to vector B.**

* Thirdly, learn how to access vector elements.

We can refer to individual elements in the vector using square brackets to provide a subscript or index, as shown below:

```c++
vector<int> A (10,5);
A[3];
```

Please note that if you initially define the vector to have n elements , **you cannot access the n+1 elements** the program will crash!!!!

A safer way to access elements is by using **vector.at(index)**. If you go out of scope, this will throw an exception and exceptions are useful when you know how to handle them.

```c++
vector<int> A (10,5);
A.at(3);
```

Bigger example, show you how to traverse the vector with a loop:
```c++
#include <iostream>
#include <vector>

using namespace std;

int main(int argc, char** argv) {
	
	/*  Initialize vector of 10 copies of the integer 5 */
	vector<int> vectorOne(10,5);
	
	/*  run through the vector and display each element, if possible */
	for (long index=0; index<20; ++index) {
		try {
			cout << "Element " << index << ": " << vectorOne.at(index) << endl;
		}
		catch (exception& e) {
			cout << "Element " << index << ": index exceeds vector dimensions." << endl;
		}
		//see how exceptions are handled?
	}
	
	return 0; //exit
}
```


## Operations on vectors

### Input 

To input data into vector, use **Vector.push_back(data)**. An empty vector will gradually put data in as you use this function more and more. In details, if i have n elements in the vector, whenever i call **vector.push_back(data)**, the vector will look if it has any empty space inside. If yes, put that data in. If no, make new space and put that data in ( it's dynamic !!! remember? ). 

```c++
vector<int> A(10); 
A.push_back(25); // will add 25 to A[0]
```

Big example incoming. This will demonstrate how **push_back** work in action. Try to guess the purpose of the codes below : 

```c++
#include <iostream>
#include <iomanip>
#include <vector>    // Needed to define vectors
using namespace std;

int main()
{
   vector<int> hours;      // hours is an empty vector
   vector<double> payRate; // payRate is an empty vector
   int numEmployees;       
   int index;              

   // Take employee number from users
   cout << "How many employees do you have? ";
   cin >> numEmployees;

   // Data input
   cout << "Enter the hours worked by " << numEmployees;
   cout << " employees and their hourly rates.\n";
   for (index = 0; index < numEmployees; index++)
   {
      int tempHours;    // To hold the number of hours entered
      double tempRate;  // To hold the payrate entered

      cout << "Hours worked by employee #" << (index + 1);
      cout << ": ";
      cin >> tempHours;
      hours.push_back(tempHours);      // Add data in vector hours.
      cout << "Hourly pay rate for employee #";
      cout << (index + 1) << ": ";
      cin >> tempRate;
      payRate.push_back(tempRate);  // Add data in vector payRate
   }

   //Output data
   cout << "Here is the gross pay for each employee:\n";
   cout << fixed << showpoint << setprecision(2);
   for (index = 0; index < numEmployees; index++)
   {
      double grossPay = hours[index] * payRate[index];
      cout << "Employee #" << (index + 1);
      cout << ": $" << grossPay << endl;
   }
   return 0;
}  
```

This is the output 

```
How many employees do you have? 3 [enter]
Enter the hours worked by 3 employees and their hourly rates.
Hours worked by employee #1: 40 [enter]
Hourly pay rate for employee #1: 12.63 [enter]
Hours worked by employee #2: 25 [enter]
Hourly pay rate for employee #2: 10.35 [enter]
Hours worked by employee #3: 45 [enter]
Hourly pay rate for employee #3: 22.65 [enter]

Here is the gross pay for each employee:
Employee #1: $505.20
Employee #2: $258.75
Employee #3: $1019.25
Press any key to continue . . .
```

### Assign 

Another way to input data into vector is using the `assign()` function.  
As its name suggests, this function assigns values to the vector. In fact, there are two versions of the assign() function : 
* The first version takes 2 [iterators](#id-section5) as parameters. 
* The second version takes 1 integer ( as the size you want ) and another data type as default input. 

For instance : 

```cpp
#include <iostream>
#include <vector>
using namespace std; 

int main ()
{
  vector<int> demo1;
  vector<int> demo2;
  vector<int> demo3;

  demo1.assign (10,68);             // assign 10 elements, each equals to 68

  vector<int>::iterator it;
  it = demo1.begin()+1;             // call an iterator to the second position of demo1

  demo2.assign (it,demo1.end());  // assign demo2 with 9 elements, each element equals to its counter part in demo1 , which is 68

  int arrayDemo[] = {1,2,3,4};
  demo3.assign (arrayDemo,arrayDemo+4);   // assigning elements using array.

  return 0;
} 
// this code will assign demo1 as {68, 68, 68, 68, 68, 68, 68, 68, 68, 68}
// demo2 as                       {68, 68, 68, 68, 68, 68, 68, 68, 68}
// demo3 as                       {1,2,3,4}
```

### Insert 

There will be cases that you want to insert something in the vector while solving a problem, not assign or input it from the beginning or construction phase. In that case, the insert() operation may come in handy. 
* Using insert is very simple as you input the position and the value. 
* You can also input multiple elements (with the same value) at once or copy the input from another container thanks to iterators.  

One thing worth noticing is inserting a single element retains the iterator, so it returns the iterator (it looks like this `iterator insert(iterator position, int value)`)
Seeing is believing : 

```cpp
#include <iostream>
#include <vector>
using namespace std; 

int main ()
{
  vector<int> myvector (2,100);   // construct a vector with 2 elements 100.
  vector<int>::iterator it;
  it = myvector.begin();

  //let's go
  // first style : iterator and value
  it = myvector.insert ( it , 200 );      // this input 200 at the beginning.  myvector is now {200, 100, 100}
  // be careful, inputting 1 element with insert() retun an iterator to maintain the validation of that iterator
  // so here we see this instead of myvector.insert(it, 200) only.



  // second style :   iterator, number-of-elements, value
  myvector.insert(it, 2 , 300);    // this input 2 elements 300 at the beginning. my vector is now {300, 300, 200, 100, 100}

  //input more than 1 element makes it no longer valid, which is why we need to construct it again
  it = myvector.begin();

  // third style : copy data from an array to insert
  int myarray [] = { 600, 700, 900 };
  myvector.insert (it, myarray, myarray+3);   // my vector is now {600, 700, 900, 300, 300, 200, 100, 100}

  return 0;

}
```

### Comparison Operators 

Applying Comparion Operators (such as ==, > , < , != , >= , <= ) on two vectors mean applying them on two vectors' elements. It will return true or false by comparing each pair of elements together. 

```cpp
int main(){
    using namespace std;   
    vector<int> v1{10, 20, 30, 40, 50};
    vector<int> v2{10, 20, 30, 40, 50};

    if(v1==v2)
        cout<<"equal";
    else
        cout<<"unequal";
}   // it returns equal 
``` 

### Size

The size of a vector is accessed via **vector.size()**. 

```c++
vector<int> A(10);
int numberOfValues = A.size(); //will equal to 10
```

Now let's take a closer look at this example 

```c++
#include <iostream>
#include <vector>
using namespace std;

// Function prototype
void showValues(vector<int>);

int main()
{
   vector<int> values;

   // Add 7 values in vector
   for (int count = 0; count < 7; count++)
      values.push_back(count * 2);
   
   //Print all the values
   showValues(values);
   return 0;
}

//**************************************************
// Pay attention to the showValue function            
// It will print to console every value of the whole vector                   
//**************************************************

void showValues(vector<int> vect)
{
   for (int count = 0; count < vect.size(); count++)
      cout << vect[count] << endl;
}  
```

The function shows you how vector **size** can be put in action. It is very useful when you want to make a loop that traverse the whole vector or control the elements of a vector (just like an array).

### Output

To get an element out of the vector, we use **vector.pop_back()**. Please note that when we use **pop_back()**, the last value of the vector will get popped out. Therefore, the vector now no longer stores that data and it is important to remember this as we should avoid direct access to this element afterwards.

Let's consider this example so that you can understand how **vector.pop_back()** is used 

```c++
using namespace std;

int main()
{
   vector<int> values;

   //Insert/Input values
   values.push_back(1);
   values.push_back(2);
   values.push_back(3);
   cout << "The size of values is " << values.size() << endl;
   
   //Here come the pop_back().
   cout << "Popping a value from the vector...\n";
   values.pop_back();
   cout << "The size of values is now " << values.size() << endl;
   
   // Continue to pop_back().
   cout << "Popping a value from the vector...\n";
   values.pop_back();
   cout << "The size of values is now " << values.size() << endl;
   
   //Continue to pop_back().
   cout << "Popping a value from the vector...\n";
   values.pop_back();
   cout << "The size of values is now " << values.size() << endl;
   return 0;
}  
```

Here's the output to the above code: 

```
The size of values is 3
Popping a value from the vector...
The size of values is now 2
Popping a value from the vector...
The size of values is now 1
Popping a value from the vector...
The size of values is now 0
Press any key to continue . . .
```

### Erase

The **Vector.erase(iterator)** will erase the desired element. However, it needs to be passed in an [iterator](#id-section5) to decide where should erasing happens. For example:

```cpp
for (int i=0; i<10; i++) {
    myvector.push_back(i+1); // 1 2 3 4 5 6 7 8 9 10
}

  // erase the 6th element
  myvector.erase (myvector.begin()+5);
  // this will erase 6 out of the vector.

  // erase the 1st element
  myvector.erase (myvector.begin());
  // this will erase 1 out of the vector 
```

It is also worth noticing that, by passing in 2 iterators, you can erase a range of elements. For example : 

```cpp
for (int i=0; i<10; i++) {
    myvector.push_back(i+1); // 1 2 3 4 5 6 7 8 9 10
}

myvector.erase(myvector.begin(), myvector.begin()+5); // will delete everything from 1 -> 6
```



### Clear 

If you want to completely delete the whole vector, or return it to its original state where no value is assigned in each element, usually your brain comes up with **pop_back()** or a loop deleting each value ( assume you desire to apply what you have learnt above ! ) . However, that costs time and generate unnecessary lines of codes where we can just use **vector.clear()** to clear all the vector data.

```c++
#include <iostream>
#include <vector>
using namespace std;

int main()
{
   vector<int> values(100);

   cout << "The values vector has "
        << values.size() << " elements.\n";
   cout << "I will call the clear member function...\n";
   values.clear();
   cout << "Now, the values vector has "
        << values.size() << " elements.\n";
   return 0;
}  
```

and guess what the output is ...

```
The values vector has 100 elements.
I will call the clear member function...
Now, the values vector has 0 elements.
Press any key to continue . . .
```

Simple as eating a cake, isn't it?
Plus, if you want to check whether the current vector is empty or not, you can call out **vector.empty()**. Here's a quick look at how to implement it : 

```c++
if(A.empty() == true){
       cout << "No values in A \n";
} 
```
### Resize

This **vector.resize(size , new_default_element)** helps you resize a vector (and set new default . Be careful when play with resize as it will result in loss of data if you seize down the vector. Consider the below example to see how resizing is put into action :

```c++
#include <iostream>
#include <vector>

using namespace std;

int main(int argc, char** argv) {
	
	/*  Initialize vector of 10 copies of the integer 5 */
	vector<int> vectorOne(10,5);
	
	/*  Display size of vector */
	cout << "Size of vector is " << vectorOne.size() << " elements." << endl;
	
	/*  run through the vector and display each element, using size() to determine index boundary */
	for (long index=0; index<(long)vectorOne.size(); ++index) {
		cout << "Element " << index << ": " << vectorOne.at(index) << endl;
	}
	
	/*  Change size of vector - element removal */
	vectorOne.resize(7);
	
	/*  Display size of vector */
	cout << "Size of vector is " << vectorOne.size() << " elements." << endl;
	
	/*  run through the vector and display each element, using size() to determine index boundary */
	for (long index=0; index<(long)vectorOne.size(); ++index) {
		cout << "Element " << index << ": " << vectorOne.at(index) << endl;
	}
	
	return 0;
}
```

This is the output :

```
Size of vector is 10 elements.
Element 0: 5
Element 1: 5
Element 2: 5                        
Element 3: 5
Element 4: 5
Element 5: 5
Element 6: 5
Element 7: 5
Element 8: 5
Element 9: 5
Size of vector is 7 elements.
Element 0: 5
Element 1: 5
Element 2: 5
Element 3: 5
Element 4: 5
Element 5: 5
Element 6: 5   
```

### Other good stuffs

* **Vector.begin()** returns an iterator to the start of the vector.
* **Vector.end()** returns an iterator to the end of the vector.
* **Vector.at(index)** returns the element at some index in the vector.
* **Vector.swap(vector2)** swap the content of two vectors.
* **Vector.front()** accesses the first element.
* **Vector.back()** accesses the last element.
* **Vector.max_size()** returns how many elements the vector can contain.
* **Vector.capacity()** returns the number of elements that the vector can hold before more space is allocated. It is very important to remember here that, unlike raw arrays, most of the memory management for vectors is performed silently during construction or manipulation of the container. The **reserve()** method only allocates memory, but leaves it uninitialized. It only affects **capacity()**, but **size()** will be unchanged. 
Consider this : 

```c++
#include <iostream>
#include <vector>
 
using namespace std;
 
int main()
{
    vector< int > my_vect;
    my_vect.reserve( 10 );
    my_vect.push_back( 1 );
    my_vect.push_back( 2 );
    my_vect.push_back( 3 );
 
    cout << my_vect.capacity() << "\n";
    cout << my_vect.size() << "\n";
 
    return 0;
}
```

The output here is : 
```
10
3
```

Now you see the difference between capacity and size although they seem to be similar to each other.
![](https://www.securecoding.cert.org/confluence/download/attachments/20087026/vector-clipped.jpg?version=1&modificationDate=1239994411000&api=v2)



## Bonus : Iterators 

Iterator is a pointer-like object. It can be increase with prefix or suffix increment, dereference with \* and compared against another operator with !=. Iterators are often fundamental when learning C++ Standard Template Library as it provide a means for accessing data stored in containers.  

Declaring an iterator is easy: 
```cpp
vector<int> IntVector;
vector<int>::iterator IntVectorIterator;
```

The common syntax is : `container<dataTypeInside>::iterator name;`  

**However**, some of you ask :  
> Why use iterators instead of indices ?  

While I was learning about this, the same question came up to me as well. The context is actually a comparison between two kinds of code like this :  

1. *Version 1*
```cpp
for(int y=0; y<someThing.size(); y++)
{
    cout<<someThing[y]<<" ";
}
```

2. *Version 2*
```cpp
for(myIterator = someThing.begin(); myIterator != something.end(); myIntVectorIterator++)
{
    cout<<*myIterator<<" ";
}
```

They do the same thing. So why do we use iterators since the first way seems friendlier, easier and more familiar (to beginners) ?  

*Because of __Performance__*

Imagine you are standing at the beginning of a train. Your job is to run from the first compartment to the last compartment, to find a passenger A. For a train that has a certain number of compartment, the job is quite easy. But for a extremely long train, counting how many compartments/passengers there are would kill you before you even do the job. Also, sometimes you dont have to reach the end to find the passenger. So why do you have to know how many compartments/passengers there are ? Why dont you just start the job and save the time.   

![](images/trainexample.jpg)  

Iterator in Cpp inherits the same logic. With iterators, you won't have to *store the size of the container* (which is a not-always-fast operation)/ For a vector, using index may still be fine ( but not recommended ) - your vector's size may be controllable. But for other containers like list, map, ... iterator is the best choice. It's more generic and plays well with **algorithms**. 

Together, **containers, iterators and algorithms** are the silver bullet of C++ STL.

----------


_This is the end!_ :smiley: _Have fun!_ :smiley:

##### Donation
[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=5ZG5Z47L2ZGYC)
A beer in your country can buy a meal in mine.