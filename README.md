Download link :https://programming.engineering/product/cs-445-data-structures-assignment-java-oop-arrays-and-generics/

# CS-445-Data-Structures-Assignment-Java-OOP-Arrays-and-Generics
CS 445 Data Structures Assignment – Java OOP, Arrays, and Generics
OVERVIEW


Purpose: To refresh your Java programming skills, to emphasize the object-oriented programming approach used in Java, and to practice working with Java arrays. Specifically, you will work with control structures, class-building, interfaces and generics to create and utilize a simple array-based data structure.

Goal 1: To design and implement a simple class ArrayDS<T> that will act as a simple data structure for accessing Java Objects. Your ArrayDS<T> class will primarily implement 2 interfaces – PrimQ<T> and Reorder. The details of these interfaces are explained in the files PrimQ.java and Reorder.java. Read these files over very carefully before implementing your ArrayDS<T> class.

Goal 2: To utilize your ArrayDS<T> class to store and manipulate arbitrary length integers. We can think of an integer as a sequence of decimal digits. For example, the number 1234 could be stored as the digit ‘1’ followed by the digit ‘2’ followed by the digit ‘3’ followed by the digit ‘4’. We will store these digits in an array. Clearly, to perform operations on a number that is stored in this fashion, we must access the digits one at a time in some systematic way. More specific details follow below.

DETAILS



Details 1: For the details on the functionality of your ArrayDS<T> class, carefully read over the files PrimQ.java, Reorder.java and Assig1A.java provided on the CourseWeb folder where you find this assignment description. You must use these files as specified and cannot remove/alter any of the code that is already written in them. There are different ways of implementing the PrimQ<T> and Reorder interface methods, some of which are more efficient than others. Try to think of the best way of implementing these methods in this assignment, but the most important thing at this point is getting them to work. A lot of pencil and paper work is recommended before actually starting to write your code. Later we will discuss the relative merits of different implementations. Your ArrayDS<T> class header should be:

public class ArrayDS<T> implements PrimQ<T>, Reorder

Assignment adapted from Dr. John Ramirez’s CS 445 class.


Important Note: The primary data within your ArrayDS<T> class must be an array. You may not use any predefined Java collection class (e.g., ArrayList) for your ArrayDS<T> data fields.

You may use the following instance variables inside the ArrayDS<T> class:

final protected T[] array; //the underlying array protected int count; //the number of items in the array

You may add other variables and named constants to follow the secure programming practices we will mention in class.

Besides the methods of PrimQ<T> and Reorder, you will also need to write the following constructors:

public ArrayDS(int capacity)

public ArrayDS(ArrayDS<T> other)

The first constructor simply initializes the underlying array to an array of size capacity, and the second constructor (copy constructor) generates a new ArrayDS that is a copy of the argument (copying all of the items inside the argument object).

Finally, you will need to override the following method:

public String toString();

This method will return a String that is the result of all of the items in the ArrayDS appended together, separated by spaces, preceded by the word Contents: (on a separate line) and followed by a new line. For example, if an ArrayDS object contains the numbers 1, 2, 3, 4, 5, 6, toString() should output:

Contents:

123456

After you have finished your coding of ArrayDS<T>, the Assig1A.java file provided for you should compile and run correctly and should give output identical to the output shown in the sample execution in A1Out.txt.

Details 2: The second part of this assignment is to write the ReallyLongInt class with the specifications as given below. You may assume all numbers will be non-negative.

Inheritance: ReallyLongInt must be a subclass of ArrayDS. However, since ArrayDS is generic while

ReallyLongInt is not generic, you should use the following header:

public class ReallyLongInt extends ArrayDS<Integer>

implements Comparable<ReallyLongInt>

Note that rather than T, the underlying element data type is now Integer. This means that the individual digits of your ReallyLongInt will be Integer objects. To avoid getting ClassCastException, don’t access array from inside the methods of ReallyLongInt. You will need to add the following two methods to ArrayDS in order to access array elements.

protected T getItem(int i) {

if (i >= count)

throw new IndexOutOfBoundsException(); return array[i];

}

protected void setItem(int i, T value) { if (i >= count)

throw new IndexOutOfBoundsException(); array[i] = value;

}

Data: The data for this class is inherited and you may not add any additional instance variables. You will certainly need method variables for the various operations but the only instance variables that you need are those inherited from ArrayDS. In order to have access inside ReallyLongInt to the data fields of ArrayDS, you will need to change their access modifiers to protected.

Operations: Your ReallyLongInt class must implement the methods shown below. Note that the compareTo() method is necessary for the Comparable interface.

private ReallyLongInt(int size)

This constructor will create as “zeroed out” ReallyLongInt with the given size. Note that this leaves the number in an inconsistent state (having leading zeros), so it should only be used within the class itself as a utility (for example, you will probably need it in your add() and subtract() methods). For this reason, it is declared as private.

public ReallyLongInt(String s)

The string s consists of a valid sequence of digits with no leading zeros (except for the number 0 itself – a special case). Insert the digits as Integer objects, such that the most significant digit is at the beginning. For example, the String “456202” would be stored in a ReallyLongInt as:

4 5 6 2 0 2

public ReallyLongInt(ReallyLongInt other)

This just requires a call to super. However, it is dependent upon a correct implementation of the copy constructor for the ArrayDS class.

public String toString()

Return a string that accurately shows the integer as we would expect to see it. Based on the way we have stored the integer, this should be accomplished by going forward through the array.

To help you out with the assignment, I have implemented the methods above for you, with comments. See the code in ReallyLongInt.java.

public ReallyLongInt add(ReallyLongInt rightOp)

Return a NEW ReallyLongInt that is the sum of the current ReallyLongInt and the parameter

ReallyLongInt, without altering the original values. For example:

ReallyLongInt X = new ReallyLongInt(“123456789”);

ReallyLongInt Y = new ReallyLongInt(“987654321”);

ReallyLongInt Z;

Z = X.add(Y);

System.out.println(X + ” + ” + Y + ” = ” + Z);

should produce the output:

123456789 + 987654321 = 1111111110

Be careful to handle carries correctly and to process the digits in the correct order. Since the numbers are stored with the most significant digit at the beginning, the add() method can be implemented by first reversing then traversing both numbers in a systematic way. You should start at the beginning of each ReallyLongInt and traverse one time while doing the addition. Also, be careful to handle numbers with differing numbers of digits.

public ReallyLongInt subtract(ReallyLongInt rightOp)

Return a NEW ReallyLongInt that is the difference of the current ReallyLongInt and the parameter ReallyLongInt. Since ReallyLongInt is specified to be non-negative, if rightOp is greater than the current ReallyLongInt, you should throw an ArithmeticException. Otherwise, subtract digit by digit (borrowing if necessary) as expected. This method is tricky because it can result in leading zeros, which we don’t want. Be careful to handle this case (and consider the tools provided by ArrayDS that will allow you to handle it). For example:

ReallyLongInt X = new ReallyLongInt(“123456”);

ReallyLongInt Y = new ReallyLongInt(“123455”);

ReallyLongInt Z;

Z = X.subtract(Y);

System.out.println(X + ” – ” + Y + ” = ” + Z);

should produce the output:

123456 – 123455 = 1

As with the add() method, be careful to handle numbers with differing numbers of digits. Also note that borrowing may extend over several digits. See RLITest.java for some example cases.

public int compareTo (ReallyLongInt rightOp)

Defined the way we expect compareTo to be defined for numbers. If one number has more digits than the other then clearly it is bigger (since there are no leading 0s). Otherwise, the numbers must be compared digit by digit. Since this requires the most significant digit to be processed first (which is at the front), we can just iterate through the digits as given.

public boolean equals(Object rightOp)

Defined the way we expect equals to be defined for objects – comparing the data and not the reference. Don’t forget to cast rightOp to ReallyLongInt so that its array can be accessed (note: the argument here is Object rather than ReallyLongInt because we are overriding equals() from the version defined in class Object). Note: This method can easily be implemented once compareTo() has been completed.

public ReallyLongInt multTenToThe(int num)

Return the result of Multiplying the current ReallyLongInt by 10num . Note that this can be done very simply through adding of 0’s.

public ReallyLongInt divTenToThe(int num)

Return the result of Dividing the current ReallyLongInt by 10num . Note that this can be done very simply through shifting.

To verify that your ReallyLongInt class works correctly, you will use it with the program RLITest.java, which is provided for you on the Assignments CourseWeb page. Your output should match that shown in RLITest.txt.

Important Note:

Both the add() and subtract() methods are tricky and have different cases to consider. For these methods especially I recommend working out some examples on paper to see what needs to be considered before actually coding them.

EXTRA CREDIT



Here are a couple non-trivial extra credit ideas. Either one done well could get you the full 15 extra credit points. However, don’t attempt either until you are confident that your required classes are working correctly.

Allow the numbers to be signed, so that we can have both positive and negative numbers. This may require an extra instance variable (for the “sign”) and will clearly affect many of your methods. If you choose this extra credit, you must submit it as a separate class (ReallyLongInt2) in addition to your original ReallyLongInt class. You must also submit a separate driver program to test / demonstrate your signed ReallyLongInt2 class.

Add a multiply() method to your ReallyLongInt class. If you implement this you should also submit a separate driver program to test / demonstrate the multiply() method.

SUBMISSION REQUIREMENTS



You must submit the following two complete, working source files:

ArrayDS.java

ReallyLongInt.java

5


The above two files must be created so that they work as described. If you create any additional files, be sure to include those as well.

The idea from your submission is that the autograder can compile and run both of the main programs (Assig1A.java and RLITest.java) from the command line WITHOUT ANY additional files or changes, so be sure to test it thoroughly before submitting it.

If you cannot get the programs working as given, clearly indicate any changes you made and clearly indicate why (e.g., “I could not get the reverse() method to work, so I eliminated code that used it”) on your Assignment Information Sheet. You will lose some credit for not getting it to work properly, but getting the main programs to work with modifications is better than not getting them to work at all. A template for the Assignment Information Sheet can be found in the assignment’s CourseWeb folder. You do not have to use this template but your sheet should contain the same information.

Note: If you use an IDE such as NetBeans, Eclipse, or IntelliJ, to develop your programs, make sure they will compile and run on the command line before submitting – this may require some modifications to your program (such as removing some package information).

RUBRICS


Please check the grading rubric on CourseWeb.

HINTS / NOTES


See file A1Out.txt to see how your output for Assig1A should look. As noted, your output when running Assig1A.java should be identical to this.

See file RLHTest.txt to see how your output for RLHTest.java should look. As noted, your output when running RLHTest.java should be identical to this.

Your ArrayDS<T> class will need to allow for a variable number of objects, up to some maximum number (set by the initial size). You can implement this by having an integer instance variable (e.g., “count”) that indicates how many slots in the ArrayDS<T> are filled. When implementing ArrayDS<T> be careful to use the “count” value rather than the array length when doing operations such as the toString() method.

In order for the Assig1A.java output to show correctly, you must override the toString() method in the ArrayDS class. You should be familiar with the toString() method from CS 0401.

Note that for the most part, all of your methods (in both interfaces) in your ArrayDS class should act on the logical data structure — accessing only the locations in the array that actually are storing data (See note 4 above).

For Javadoc comments and code style, please refer to Appendix A of the textbook.

6
