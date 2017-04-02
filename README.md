# Operators

### User-defined types can overload [the ~ operator](https://msdn.microsoft.com/en-us/library/d2bd4x66.aspx). For more information, see operator. Operations on integral types are generally allowed on enumeration.

Example
```C#
    class BWC
    {
        static void Main()
        {
            int[] values = { 0, 0x111, 0xfffff, 0x8888, 0x22000022 };
            foreach (int v in values)
            {
                Console.WriteLine("~0x{0:x8} = 0x{1:x8}", v, ~v);
            }
        }
    }
    /*
    Output:
    ~0x00000000 = 0xffffffff
    ~0x00000111 = 0xfffffeee
    ~0x000fffff = 0xfff00000
    ~0x00008888 = 0xffff7777
    ~0x22000022 = 0xddffffdd
    */
    
 ```
 
 ### The [% operator](https://msdn.microsoft.com/en-us/library/0w4e0fzs.aspx) computes the remainder after dividing its first operand by its second. All numeric types have predefined remainder operators.

User-defined types can overload the % operator (see operator). When a binary operator is overloaded, the corresponding assignment operator, if any, is also implicitly overloaded.
Example
```C#
    class MainClass6
    {
        static void Main()
        {
            Console.WriteLine(5 % 2);       // int
            Console.WriteLine(-5 % 2);      // int
            Console.WriteLine(5.0 % 2.2);   // double
            Console.WriteLine(5.0m % 2.2m); // decimal
            Console.WriteLine(-5.2 % 2.0);  // double
        }
    }
    /*
    Output:
    1
    -1
    0.6
    0.6
    -1.2
    */
```

### The [& operator](https://msdn.microsoft.com/en-us/library/sbf85k1c.aspx) can function as either a unary or a binary operator.

The unary & operator returns the address of its operand (requires unsafe context).
Binary & operators are predefined for the integral types and bool. For integral types, & computes the logical bitwise AND of its operands. For bool operands, & computes the logical AND of its operands; that is, the result is true if and only if both its operands are true.
The & operator evaluates both operators regardless of the first one's value. For example:
```C#
            int i = 0;
            if (false & ++i == 1)
            {
                // i is incremented, but the conditional
                // expression evaluates to false, so
                // this block does not execute.
            }
```
User-defined types can overload the binary & operator (see operator). Operations on integral types are generally allowed on enumeration. When a binary operator is overloaded, the corresponding assignment operator, if any, is also implicitly overloaded.
Example
```C#
    class BitwiseAnd
    {
        static void Main()
        {
            // The following two statements perform logical ANDs.
            Console.WriteLine(true & false); 
            Console.WriteLine(true & true);  

            // The following line performs a bitwise AND of F8 (1111 1000) and
            // 3F (0011 1111).
            //    1111 1000
            //    0011 1111
            //    ---------
            //    0011 1000 or 38
            Console.WriteLine("0x{0:x}", 0xf8 & 0x3f); 
        }
    }
    // Output:
    // False
    // True
    // 0x38
  ```
  ### Binary [| operators](https://msdn.microsoft.com/en-us/library/kxszd0kx.aspx) are predefined for the integral types and bool. For integral types, | computes the bitwise OR of its operands. For bool operands, | computes the logical OR of its operands; that is, the result is false if and only if both its operands are false.

User-defined types can overload the | operator (see operator).
Example
```C#
    class OR
    {
        static void Main()
        {
            Console.WriteLine(true | false);  // logical or
            Console.WriteLine(false | false); // logical or
            Console.WriteLine("0x{0:x}", 0xf8 | 0x3f);   // bitwise or
        }
    }
    /*
    Output:
    True
    False
    0xff
    */
 ``` 
 ### Binary [^ operators](https://msdn.microsoft.com/en-us/library/zkacc7k1.aspx) are predefined for the integral types and bool. For integral types, ^ computes the bitwise exclusive-OR of its operands. For bool operands, ^ computes the logical exclusive-or of its operands; that is, the result is true if and only if exactly one of its operands is true.

User-defined types can overload the ^ operator (see operator). Operations on integral types are generally allowed on enumeration.
Example
```C#
    class XOR
    {
        static void Main()
        {
            // Logical exclusive-OR

            // When one operand is true and the other is false, exclusive-OR 
            // returns True.
            Console.WriteLine(true ^ false);
            // When both operands are false, exclusive-OR returns False.
            Console.WriteLine(false ^ false);
            // When both operands are true, exclusive-OR returns False.
            Console.WriteLine(true ^ true);


            // Bitwise exclusive-OR

            // Bitwise exclusive-OR of 0 and 1 returns 1.
            Console.WriteLine("Bitwise result: {0}", Convert.ToString(0x0 ^ 0x1, 2));
            // Bitwise exclusive-OR of 0 and 0 returns 0.
            Console.WriteLine("Bitwise result: {0}", Convert.ToString(0x0 ^ 0x0, 2));
            // Bitwise exclusive-OR of 1 and 1 returns 0.
            Console.WriteLine("Bitwise result: {0}", Convert.ToString(0x1 ^ 0x1, 2));

            // With more than one digit, perform the exclusive-OR column by column.
            //    10
            //    11
            //    --
            //    01
            // Bitwise exclusive-OR of 10 (2) and 11 (3) returns 01 (1).
            Console.WriteLine("Bitwise result: {0}", Convert.ToString(0x2 ^ 0x3, 2));

            // Bitwise exclusive-OR of 101 (5) and 011 (3) returns 110 (6).
            Console.WriteLine("Bitwise result: {0}", Convert.ToString(0x5 ^ 0x3, 2));

            // Bitwise exclusive-OR of 1111 (decimal 15, hexadecimal F) and 0101 (5)
            // returns 1010 (decimal 10, hexadecimal A).
            Console.WriteLine("Bitwise result: {0}", Convert.ToString(0xf ^ 0x5, 2));

            // Finally, bitwise exclusive-OR of 11111000 (decimal 248, hexadecimal F8)
            // and 00111111 (decimal 63, hexadecimal 3F) returns 11000111, which is 
            // 199 in decimal, C7 in hexadecimal.
            Console.WriteLine("Bitwise result: {0}", Convert.ToString(0xf8 ^ 0x3f, 2));
        }
    }
    /*
    Output:
    True
    False
    False
    Bitwise result: 1
    Bitwise result: 0
    Bitwise result: 0
    Bitwise result: 1
    Bitwise result: 110
    Bitwise result: 1010
    Bitwise result: 11000111
    */
```
The computation of 0xf8 ^ 0x3f in the previous example performs a bitwise exclusive-OR of the following two binary values, which correspond to the hexadecimal values F8 and 3F:
```C#
1111 1000
0011 1111
```
The result of the exclusive-OR is 1100 0111, which is C7 in hexadecimal.


### The [left-shift assignment operator](https://msdn.microsoft.com/en-us/library/ayt2kcfb.aspx).

An expression of the form
```C#
x <<= y  
```
is evaluated as
```C#
x = x << y  
```
except that x is only evaluated once. The << operator shifts x left by the number of bits specified by y.
The <<= operator cannot be overloaded directly, but user-defined types can overload the << operator.
Example
```C#
    class MainClass9
    {
        static void Main()
        {
            int a = 1000;
            a <<= 4;
            Console.WriteLine(a);
        }
    }
    /*
    Output:
    16000
    */
```
### The [right-shift assignment operator](https://msdn.microsoft.com/en-us/library/23as4533.aspx).

An expression of the form
```C#
x >>= y  
```
is evaluated as
```C#
x = x >> y  
```
except that x is only evaluated once. The >> operator shifts x right by an amount specified by y.
The >>= operator cannot be overloaded directly, but user-defined types can overload the >> operator (see operator).
Example
```C#
    class MainClass8
    {
        static void Main()
        {
            int a = 1000;
            a >>= 4;
            Console.WriteLine(a);
        }
    }
    /*
    Output:
    62
    */
```
### The [-> operator](https://msdn.microsoft.com/en-us/library/s8bz4d5h.aspx) combines pointer dereferencing and member access.

An expression of the form,
```C#
x->y  
```
(where x is a pointer of type T* and y is a member of T) is equivalent to,
```C#
(*x).y  
```
The -> operator can be used only in code that is marked as unsafe.
The -> operator cannot be overloaded.
Example
```C#
    // compile with: /unsafe

    struct Point
    {
        public int x, y;
    }

    class MainClass12
    {
        unsafe static void Main()
        {
            Point pt = new Point();
            Point* pp = &pt;
            pp->x = 123;
            pp->y = 456;
            Console.WriteLine("{0} {1}", pt.x, pt.y);
        }
    }
    /*
    Output:
    123 456
    */
 ```
 
 ### The [=> token is called the lambda operator](https://msdn.microsoft.com/en-us/library/bb311046.aspx). It is used in lambda expressions to separate the input variables on the left side from the lambda body on the right side. Lambda expressions are inline expressions similar to anonymous methods but more flexible; they are used extensively in LINQ queries that are expressed in method syntax. For more information, see Lambda Expressions.
 
The following example shows two ways to find and display the length of the shortest string in an array of strings. The first part of the example applies a lambda expression (w => w.Length) to each element of the words array and then uses the Min`<TSource>` method to find the smallest length. For comparison, the second part of the example shows a longer solution that uses query syntax to do the same thing.

```C#
string[] words = { "cherry", "apple", "blueberry" };  
  
// Use method syntax to apply a lambda expression to each element  
// of the words array.   
int shortestWordLength = words.Min(w => w.Length);  
Console.WriteLine(shortestWordLength);  
  
// Compare the following code that uses query syntax.  
// Get the lengths of each word in the words array.  
var query = from w in words  
            select w.Length;  
// Apply the Min method to execute the query and get the shortest length.  
int shortestWordLength2 = query.Min();  
Console.WriteLine(shortestWordLength2);  
  
// Output:   
// 5  
// 5  
```

The => operator has the same precedence as the assignment operator (=) and is right-associative.
You can specify the type of the input variable explicitly or let the compiler infer it; in either case, the variable is strongly typed at compile time. When you specify a type, you must enclose the type name and the variable name in parentheses, as the following example shows.
```C#
int shortestWordLength = words.Min((string w) => w.Length);  
```
Example
The following example shows how to write a lambda expression for the overload of the standard query operator Enumerable.Where`<TSource>` that takes two arguments. Because the lambda expression has more than one parameter, the parameters must be enclosed in parentheses. The second parameter, index, represents the index of the current element in the collection. The Where expression returns all the strings whose lengths are less than their index positions in the array.
```C#
static void Main(string[] args)  
{  
    string[] digits = { "zero", "one", "two", "three", "four", "five",   
            "six", "seven", "eight", "nine" };  
  
    Console.WriteLine("Example that uses a lambda expression:");  
    var shortDigits = digits.Where((digit, index) => digit.Length < index);  
    foreach (var sD in shortDigits)  
    {  
        Console.WriteLine(sD);  
    }  
  
    // Output:  
    // Example that uses a lambda expression:  
    // five  
    // six  
    // seven  
    // eight  
    // nine  
}  
```

### The [?? operator](https://msdn.microsoft.com/en-us/library/ms173224.aspx) is called the null-coalescing operator. It returns the left-hand operand if the operand is not null; otherwise it returns the right hand operand.

A nullable type can represent a value from the type’s domain, or the value can be undefined (in which case the value is null). You can use the ?? operator’s syntactic expressiveness to return an appropriate value (the right hand operand) when the left operand has a nullible type whose value is null. If you try to assign a nullable value type to a non-nullable value type without using the ?? operator, you will generate a compile-time error. If you use a cast, and the nullable value type is currently undefined, an InvalidOperationException exception will be thrown.
For more information, see Nullable Types.
The result of a ?? operator is not considered to be a constant even if both its arguments are constants.
Example
```C#
    class NullCoalesce
    {
        static int? GetNullableInt()
        {
            return null;
        }

        static string GetStringValue()
        {
            return null;
        }

        static void Main()
        {
            int? x = null;

            // Set y to the value of x if x is NOT null; otherwise,
            // if x = null, set y to -1.
            int y = x ?? -1;

            // Assign i to return value of the method if the method's result
            // is NOT null; otherwise, if the result is null, set i to the
            // default value of int.
            int i = GetNullableInt() ?? default(int);

            string s = GetStringValue();
            // Display the value of s if s is NOT null; otherwise, 
            // display the string "Unspecified".
            Console.WriteLine(s ?? "Unspecified");
        }
    }
```

### 
