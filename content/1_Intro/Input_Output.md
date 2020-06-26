---
id: io
title: Input & Output
author: Darren Yao
description: Demonstrates how to read input and print output for USACO contests.
---

## Additional Reading

 - CSES 1.2
 - [PAPC 2.4](http://www.csc.kth.se/~jsannemo/slask/main.pdf)

## Standard I/O

In most websites (such as CodeForces and CSES), input and output are **standard**.

### C++

The [<iostream\>](http://www.cplusplus.com/reference/iostream/) library suffices. 

```cpp
#include <iostream>
using namespace std;

int main() {
    int x; cin >> x;
    cout << "FOUND " << x << "\n";
}
```

### Java

In your CS classes, you've probably implemented input and output using standard input and standard output, or using [`Scanner`](https://docs.oracle.com/javase/7/docs/api/java/util/Scanner.html) to read input and `System.out.print` to print output. These methods work, but `Scanner` and `System.out.print` are slow when we have to handle inputting and outputting tens of thousands of lines. Thus, we use `BufferedReader` and `PrintWriter` instead, which are faster because they buffer the input and output and handle it all at once as opposed to parsing each line individually. 

Here is a Java template for input and output, which is effectively a faster Scanner. We import the entire `util` and `io` libraries for ease of use.

<spoiler title="Standard I/O">

```java
import java.io.*;
import java.util.*;

public class template {
    static class InputReader {
        BufferedReader reader;
        StringTokenizer tokenizer;

        public InputReader(InputStream stream) {
            reader = new BufferedReader(new InputStreamReader(stream), 32768);
            tokenizer = null;
        }

        String next() { // reads in the next string
            while (tokenizer == null || !tokenizer.hasMoreTokens()) {
                try {
                    tokenizer = new StringTokenizer(reader.readLine());
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }
            return tokenizer.nextToken();
        }

        public int nextInt() { // reads in the next int
            return Integer.parseInt(next());
        }

        public long nextLong() { // reads in the next long
            return Long.parseLong(next());
        }

        public double nextDouble() { // reads in the next double
            return Double.parseDouble(next());
        }
    }

    static InputReader r = new InputReader(System.in);
    static PrintWriter pw = new PrintWriter(System.out);

    public static void main(String[] args) {

        // YOUR CODE HERE

        pw.close(); // flushes the output once printing is done
    }
}
```

</spoiler>

Here's a brief description of the methods in our `InputReader` class, with an instance `r`, and `PrintWriter` with an instance `pw`.


| Method             | Description                                                         |
| ------------------ | ------------------------------------------------------------------- |
| `r.next()`         | Reads the next token (up to a whitespace) and returns a `String`    |
| `r.nextInt()`      | Reads the next token (up to a whitespace) and returns as an `int`   |
| `r.nextLong()`     | Reads the next token (up to a whitespace) and returns as a `long`   |
| `r.nextDouble()`   | Reads the next token (up to a whitespace) and returns as a `double` |
| `pw.println()`     | Prints the argument to designated output stream and adds newline    |
| `pw.print()`       | Prints the argument to designated output stream                     |


## File I/O

In USACO, input is read from a file called `problemname.in`, and output is printed to a file called `problemname.out`. Note that you'll have to rename the `.in` and `.out` files. For example, for [this problem](http://www.usaco.org/index.php?page=viewproblem2&cpid=1035), you would replace `problemname` with `socdist1` to get `socdist1.in` and `socdist1.out`.

In order to test a program, create a file called `problemname.in`, and then run the program. The output will be printed to `problemname.out`.

## C++

You will need the [<cstdio\>](http://www.cplusplus.com/reference/cstdio/) or the [<fstream\>](http://www.cplusplus.com/reference/fstream/) library. Essentially, replace every instance of the word `problemname` in the word below with the input/output file name, which should be given in the problem. 

Below, we have included C++ templates for input and output. We use `using namespace std;` so that we don't have to preface standard library functions with `std::` each time we use them.

If `<cstdio>` is used: 

```cpp
#include <cstdio>
using namespace std;

int main() {
    freopen("problemname.in", "r", stdin);
    freopen("problemname.out", "w", stdout);
    // rest of your code ...
}
```

If `<fstream>` is used: (Note that you cannot use C-style I/O (`scanf`, `printf`) with this method): 

```cpp
#include <fstream>
using namespace std;

int main() {
    ifstream fin("problemname.in");
    ofstream fout("problemname.out");
    // rest of your code ...
}
```

## Java

We can modify the template above to support file I/O.

<spoiler title="File I/O">

```java
import java.util.*;
import java.io.*;

public class template {
    static class InputReader {
        BufferedReader reader;
        StringTokenizer tokenizer;

        public InputReader() throws FileNotFoundException {
            reader = new BufferedReader(new FileReader("template.in"));
            tokenizer = null;
        }

        String next() { // reads in the next String
            while (tokenizer == null || !tokenizer.hasMoreTokens()) {
                try {
                    tokenizer = new StringTokenizer(reader.readLine());
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }
            return tokenizer.nextToken();
        }

        public int nextInt() { // reads in the next int
            return Integer.parseInt(next());
        }

        public long nextLong() { // reads in the next long
            return Long.parseLong(next());
        }

        public double nextDouble() { // reads in the next double
            return Double.parseDouble(next());
        }
    }

    public static void main(String[] args) throws FileNotFoundException, IOException {

        InputReader r = new InputReader();
        PrintWriter pw = new PrintWriter(new BufferedWriter(new FileWriter("template.out")));

        // YOUR CODE HERE
        
        pw.close(); // flushes the output once printing is done
    }
}
```

</spoiler>

Here's an example to show how input/output works. Let's say we want to write a program that takes three numbers as input and prints their sum.

```java
// InputReader template code above
static InputReader r = new InputReader(System.in);
static PrintWriter pw = new PrintWriter(System.out);

public static void main(String[] args) {
    int a = r.nextInt();
    int b = r.nextInt();
    int c = r.nextInt()
    pw.println(a + b + c);
    pw.close();
}
```