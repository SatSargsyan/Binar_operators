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
