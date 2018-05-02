# Must-Have Extensions

The "must-haves" are those extensions that prevail our coding and projects. We hope these simple yet thoughtful "must-haves" would bring better consistency, readability and productivity to your code and project as well. This category currently includes:

[1. Consistent Containment Check](#ConsistentContainmentCheck)

[3. Consistent Emptiness Check](#ConsistentEmptinessCheck)

[7. Value Swap](#ValueSwap)

### <a name="ConsistentContainmentCheck"></a> 1. Consistent Containment Check for Collections and Strings -- The "In" Method

Instead of "_a.Contains(b)_", we provide an alternative "_b.In(a)_". If "_a_" is a collection, the the method checks if "_b_" is an element in "_a_"; if "_a_" is a dictionary, then the method checks if "_b_" is a key in "_a_". This "In" method is somewhat "python" style, **_shorter_** and **_more consistent_**; besides that, it returns _false_ for null reference.

```c#
var arr = new[] {1,2,3};
if (1.In(arr)) // equivalent to arr.Contains(1)
  Do something...

var dict = new Dictionary<string, int> { { "a", 1 } };
if ("a".In(dict)) // equivalent to dict.ContainsKey("a")
  Do something...

arr = null;
1.In(arr); // returns false
1.NotIn(arr); // returns true

dict = null;
"a".In(dict); // returns false
"a".NotIn(dict); // returns true
```

We also provide "InAny" and "InAll".

```c#
1.InAny(new []{1,2,3}, new[]{2,3,4}); // returns true
1.InAll(new []{1,2,3}, new[]{2,3,4}); // returns false
```

The same extension is added for string.

```c#
'c'.In("string to check"); // returns true
'c'.NotIn("string to check"); // returns false
'c'.InAll("string to check", "another string"); // returns false
'c'.InAny("string to check", "another string"); // returns true
```

**_In_**: returns _true_ if the element to check is contained in an array/list/collection/string, or a key of a dictionary.

**_NotIn_**: negation of **_In_**.

**_InAny_**: returns _true_ if the element to check is contained in any of the provided arrays/lists/collections/strings.

**_InAll_**: returns _true_ if the element to check is contained in all of the provided arrays/lists/collections/strings.

### <a name="ConsistentEmptinessCheck"></a> 3. Consistent Emptiness Check for Collections & Strings

Although incredibly useful, the emptiness of an array or a collection has to be checked in a clumsy way, even for today after 10 years.

```c#
var arr = new int[] {1,2,3};
if (arr != null && arr.Length != 0) // NOTE: the new syntax "arr?.Length != 0" will not do the check as desired!
  Do something...
  
var list = new List<int> {1,2,3};
if (list != null && arr.Count != 0) // NOTE: have to use a different property "Count"
  Do something...
  
var str = "abc";
if (!string.IsNullOrEmpty(str)) // another style of emptiness check, inconsistent with all others
  Do something...
```

Now with the extension, above can be greatly simplified and more readable. The method is added to both arrays and collections.

```c#
var arr = new int[] {1,2,3};
if (arr.IsNotNullOrEmpty())
  Do something...
  
var list = new List<int> { 1,2,3};
if (list.IsNotNullOrEmpty())
  Do something...
  
var dict = new Dictionary<string, int> { { "a", 1 } };
if (dict.IsNotNullOrEmpty())
  Do something...
  
var str = "abc";
if (str.IsNotNullOrEmpty())
  Do something...
```

**_IsNullOrEmpty_**: Returns true if a collection/string is a null reference or is an empty collection/string.

**_IsNotNullOrEmpty_**: the negation of **_IsNullOrEmpty_**.

**_IsEmpty_**: Returns true if a collection/string is an empty collection/string (throws an NullReferenceException if it is a null reference).

**_IsNotEmpty_**: the negation of **_IsEmpty_**.

**_IsEmptyOrBlank_**: Returns true if a string is an empty string or contains only white-space characters (throws an NullReferenceException if it is a null reference).

**_IsNotEmptyOrBlank_**: the negation of **_IsEmptyOrBlank_**, for strings only.

**_IsNullOrEmptyOrBlank_**: Returns true if a the string is a null reference, or is an empty string, or is a string with only white-sapce characters.

**_IsNotNullOrEmptyOrBlank_**: the negation of **_IsNullOrEmptyOrBlank_**, for strings only.

### <a name="ValueSwap"></a>7. Value Swap

Swapping two values have been an annoying issue that disrupts code readability. The following extensions address this problem. It is implemented by efficient bit operations when possible.

```c#
var a = 1;
var b = 2;
a.Swap(ref b);
Console.WriteLine(a); // prints 2
Console.WriteLine(b); // prints 1

var t1 = DateTime.Now;
var t2 = new DateTime(2010, 10, 22);
t1.Swap(ref t2);
Console.WriteLine(t1); // prints "[10/22/2010 12:00:00 AM]"
Console.WriteLine(t2); // prints the recorded time
```

Due to complier limitation, currently the extension only supports value types or structs. For reference type, you could consider use _Swapper.Swap_ static method.

```c#
var a = "123";
var b = "456";
Swapper.Swap(ref a, ref b); // due to compiler limitation, a static method has to be used for reference types
```

**_Swap_**: Swaps the current value of struct types with another value. 
