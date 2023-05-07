Download Link: https://assignmentchef.com/product/solved-pl-homework1
<br>
Part I : Matrix

<ol>

 <li>Write a class Column_Major_Matrix that has a member all_column which is of type vector&lt;vector&lt;T&gt;&gt;</li>

 <li>Write a class Row_Major_Matrix that has a member all_row which is of type vector&lt;vector&lt;T&gt;&gt;</li>

 <li>Provide a constructor for each class that takes arguments to specify the dimensions (e.g., Column_Major_Matrix&lt;int&gt; cc1 (1000, 1000); ), and fills up all elements by randomly generated values of type T.</li>

 <li>Provide getter/setter function to access each column and row by an index.</li>

 <li>Overload copy/assignment and move copy/assignment operator to allow the following in the main function:</li>

</ol>

Column_Major_Matrix&lt;int&gt; cc1 (1000, 1000);

Row_Major_Matrix&lt;int&gt; rr1( 1000, 1000);

Column_Major_Matrix&lt;int&gt; cc2 (cc1);

Row_Major_Matrix&lt;int&gt; rr2 = (rr1);

Column_Major_Matrix&lt;int&gt; cc3 = std::move( cc2 );

Row_Major_Matrix&lt;int&gt; rr3 = std::move( rr2 );

<ol>

 <li>Overload operator* in Row_Major_Matrix to allow calculation of the product of a Row_Major_Matrix instance to a Column_Major_Matrix instance, and return the resultant product as a Row_Major_Matrix.</li>

 <li>Overload operator* in Column_Major_Matrix to allow calculation of the product of a Column_Major_Matrix instance to a Row_Major_Matrix instance, and return the resultant product as a</li>

 <li>Write type conversion operators (i.e., operator Row_Major_Matrix() and operator Column_Major_Matrix() ) to allow implicit type conversion between Row_Major_Matrix and Column_Major_Matrix. Show it works by:</li>

</ol>

Column_Major_Matrix&lt;int&gt; cc (55, 1000);

Row_Major_Matrix&lt;int&gt; rr (1000, 66);

Row_Major_Matrix&lt;int&gt; rr = cc*rr;

<ol>

 <li>Overload operator% to use exactly 10 threads to multiplex the multiplication, and use std::chrono to show the speedup w/ and w/o multithreading.</li>

</ol>

Part II : Thread pool

<ol>

 <li>Design a thread pool class with following features:

  <ol>

   <li>Allow users to send jobs into the pool</li>

   <li>Allow any kind of callable objects as jobs               Maintain a job queue to store unfinished jobs</li>

   <li>                      Hint: element type: std::function/std::bind or package_task</li>

   <li>Have 5 threads always waiting for new jobs. Each thread will keep a record of total running time throughout the lifespan of the thread.</li>

   <li>Threads are terminated(joined) only when the thread pool is destructed. The total running time of each thread will be shown on the screen upon destruction along with the std::thread::id.               Use condition variable and mutex to notify threads</li>

  </ol></li>

</ol>

to do works




<ol start="2">

 <li>Write one function (named print_1), which can generate a random integer number and then print out ‘1’ if the number is an odd number otherwise ‘0’. Note that cout is also a shared resource.</li>

</ol>




<ol start="3">

 <li>Write a print_2 functor, which simply prints “2” on the screen. Use conditional variable to ensure that print_2 functor can only be executed when there is no more print_1 job to be executed.</li>

 <li>In main, first send 496 functions and then 4 functors into the pool.</li>

</ol>

#include&lt;queue&gt;

#include&lt;functional&gt;

#include&lt;iostream&gt;

Void add()

{

std::cerr&lt;&lt;“1”&lt;&lt;std::endl;

}




struct ADD

{

void operator()()

{

std::cerr&lt;&lt;”2”&lt;&lt;std::endl;

}

};




int main(void)

{

ADD a;

std::queue&lt; std::function&lt;void(void)&gt; &gt; jobs;             jobs.push( std::bind(add) );                 jobs.push( std::bind( std::bind(a) ) );

jobs.push( std::bind(a) );




while(!jobs.empty() )

{

jobs.front()();

jobs.pop();

}

return 0;

}


