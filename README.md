# Cryptography Solver for Discrete Math

####*This library is also implemented on TI-84, the graphing calculator. Please contact me if you need a copy of it.*

##Introduction
This is an extensible Java API to encrypt/decrypt strings by using simple ciphers introduced in the Discrete Math module, including:
<ul>
  <li>Caesar cipher</li>
  <li>Affine cipher</li>
  <li>Vigenere cipher</li>
  <li>One time pad</li>
  <li>RSA</li>
</ul>

There is also a `DiscreteMath` class backing all the necessary calculations, including
* Euclidean algorithm
* Extended Euclidean algorithm
* Greatest common divisor
* Modular exponentiation
* Modular inverse

##User Guide
###Encoding
Each ```Encoding``` object is a bi-map between ```Integer``` and ```Character```. There are two built-in encoding schemes.

```Encoding.DEFAULT``` is the default case-insensitive scheme used in most textbooks.
```
+-----+----+
|char | int|
|-----+----|
|a/A  |   0|
|b/B  |   1|
|...  | ...|
|z/Z  |  25|
+-----+----+
```

```Encoding.ASCII``` represents the well-known ASCII encoding.

###Encode/Decode
To perform a encode/decode, we need to get an ```Encoding``` instance then call the methods on it. For example, if we want to decode the string ```"programmingisfun"``` using the default encoding scheme, simply write

```java
int[] result = Encoding.DEFAULT.decode("programmingisfun");
```

Then the content in the ```result``` will be

```[15, 17, 14, 6, 17, 0, 12, 12, 8, 13, 6, 8, 18, 5, 20, 13]```

###Crypto
The built-int ```Crypto``` objects can be accessed from the static factory class ```CryptoFactory```. 

For example, to get one for the Affine cipher, which has a pair of keys `3` and `5`, and a divisor `26`, simple write

```java
Crypto affine = CryptoFactory.affine(3, 5, 26);
```

###Encryption/Decryption
If we combine the previous two sections together, we'll get how to perform a encryption/decryption.

For example, if we want to encrypt the string ```"programmingisfun"``` in a way that
<ul>
  <li>Using the default encoding scheme</li>
  <li>Using the Caesar cipher</li>
  <li>The key is 15</li>
</ul>

simply write

```java
Crypto caesar = CryptoFactory.caesar(5, 26); //key and divisor respectively
String cipher = Encoding.DEFAULT.encrypt("programmingisfun", caesar);
```
The result string ```cipher``` should have a content of ```"uwtlwfrrnslnxkzs"```.

###Define your own encoding scheme
There are two constructors in the `Encoding` class:
* `public Encoding(Map<Character, Integer> mapping)`
* `public Encoding(Map<Character, Integer> mapping, boolean ignoreCase)`

If you already have a `Map<Character, Integer>`, you can use either of the constructors to create a new `Encoding` object.

###Define your own crypto scheme
The ```Crypto``` interface requires its implementation to provide two methods: 
* ```int[] decrypt(int[] y)```
* ```int[] encrypt(int[] x)``` 

So, simply write your own class that `implements` this interface, and do define these two methods. You may ask for more data (e.g. key, divisor) in the constructor.

##More Resources
Please read the javadoc for more detailed information.
