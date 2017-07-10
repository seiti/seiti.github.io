---
layout: post
title: Exceções do .Net
date: '2010-07-07 18:22:48'
---


Uma lista de exceções úteis para utilizar em seu sistema, sem ter que criar sempre outra classe e escrever mais código.

Ultimamente tenho pensado numa programação Zen: o melhor código é o não-código. Quanto menos código você escrever, menos terá para manter, menos terá para entender, menos terá para depurar. Ou talvez esteja exacerbando apenas a [melhor qualidade de um programador](http://seiti.eti.br/blog/?p=276).

Chega de papo-furado, segue a lista (todas no namespace <tt>System</tt>):

<table><tr><td> ApplicationException </td><td> The exception that is thrown when a non-fatal application error occurs. </td></tr><tr><td> ArgumentException </td><td> The exception that is thrown when one of the arguments provided to a method is not valid. </td></tr><tr><td>ArgumentNullException

</td><td>The exception that is thrown when a null reference (Nothing in Visual Basic) is passed to a method that does not accept it as a valid argument.

</td></tr><tr><td>ArgumentOutOfRangeException

</td><td>The exception that is thrown when the value of an argument is outside the allowable range of values as defined by the invoked method.

</td></tr><tr><td> ArithmeticException </td><td>The exception that is thrown for errors in an arithmetic, casting, or conversion operation.

</td></tr><tr><td>ArrayTypeMismatchException

</td><td>The exception that is thrown when an attempt is made to store an element of the wrong type within an array.

</td></tr><tr><td> FieldAccessException </td><td>The exception that is thrown when there is an invalid attempt to access a private or protected field inside a class.

</td></tr><tr><td> FormatException </td><td>The exception that is thrown when the format of an argument does not meet the parameter specifications of the invoked method.

</td></tr><tr><td> IndexOutOfRangeException </td><td>The exception that is thrown when an attempt is made to access an element of an array with an index that is outside the bounds of the array. This class cannot be inherited.

</td></tr><tr><td>InvalidOperationException

</td><td>The exception that is thrown when a method call is invalid for the object’s current state.

</td></tr><tr><td> NotFiniteNumberException </td><td>The exception that is thrown when a floating-point value is positive infinity, negative infinity, or Not-a-Number (NaN).

</td></tr><tr><td> NotImplementedException </td><td>The exception that is thrown when a requested method or operation is not implemented.

</td></tr><tr><td> NotSupportedException </td><td>The exception that is thrown when an invoked method is not supported, or when there is an attempt to read, seek, or write to a stream that does not support the invoked functionality.

</td></tr><tr><td> NullReferenceException </td><td>The exception that is thrown when there is an attempt to dereference a null object reference.

</td></tr><tr><td> ObjectDisposedException </td><td>The exception that is thrown when an operation is performed on a disposed object.

</td></tr><tr><td>PlatformNotSupportedException

</td><td>The exception that is thrown when a feature does not run on a particular platform.

</td></tr><tr><td>RankException

</td><td>The exception that is thrown when an array with the wrong number of dimensions is passed to a method.

</td></tr><tr><td>SystemException

</td><td>Defines the base class for predefined exceptions in the namespace.

</td></tr><tr><td>TimeoutException

</td><td>The exception that is thrown when the time allotted for a process or operation has expired.

</td></tr><tr><td>TypeInitializationException

</td><td>The exception that is thrown as a wrapper around the exception thrown by the class initializer. This class cannot be inherited.

</td></tr><tr><td>UnauthorizedAccessException

</td><td>The exception that is thrown when the operating system denies access because of an I/O error or a specific type of security error.

</td></tr></table>Fonte: [http://mikevallotton.wordpress.com/2009/07/08/net-exceptions-all-of-them/](http://mikevallotton.wordpress.com/2009/07/08/net-exceptions-all-of-them/)


