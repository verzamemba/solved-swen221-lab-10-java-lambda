Download Link: https://assignmentchef.com/product/solved-swen221-lab-10-java-lambda
<br>
The purpose of this Tutorial is to sharpen your understanding of Java Lambda. There are three simple exercises, that can be completed independently.

The first exercise uses Stream.flatMap. Both map and flatMap can be applied to a Stream<em>&lt;</em>T<em>&gt; </em>and they both return a Stream<em>&lt;</em>R<em>&gt;</em>; The difference between Stream.map and Stream.flatMap is that the <em>map lambda </em>produces one output value for each input value, whereas the <em>flatMap lambda </em>produces an arbitrary number (zero or more) values for each input value. This is obtained by making the <em>flatmap lambda </em>returning a Stream<em>&lt;</em>R<em>&gt; </em>result. Then flatmap itself takes all those streams and condenses them down to a single stream.

For example, the following code output two times all the positive numbers and filter out all the negatives:

myList . stream (). flatMap (

i−<em>&gt;</em>{

i f            ( i <em>&gt;</em>=0){return Stream . of ( i , i );}

return Stream . empty ();

}). collect ( Collectors . toList ());

<h1>1           FilterClass</h1>

Given a stream, one common operation is to filter only the ones of a certain type; this is usually obtained by the following code

List<em>&lt;</em>Foo<em>&gt;</em>res=data . stream ()

. f i l t e r (e−<em>&gt;</em>e instanceof Foo)

.map(e−<em>&gt;</em>(Foo)e)

. collect ( Collectors . toList ());

This is a little sub optimal, since we have to write two operations (filter and map) and we have to repeat the name of the class. It is possible to use flatMap and write an opportune method

FilterClass .isInstanceOf(class) so that

List<em>&lt;</em>Foo<em>&gt;</em>res=data . stream ()

. flatMap ( FilterClass . isInstanceOf (Foo . class ))

. collect ( Collectors . toList ());

Would have the same behaviour of the code shown before.

Your task is to complete the implementation of the method FilterClass .isInstanceOf(class). You should now see the correlated tests passing.

<h1>2           Simplify reflection</h1>

Using reflection may fill our code with repetitive try-catching, as in the iconic code here:

try {/∗example∗/ return String . class . getMethod(” toString ”). invoke (””);

}

catch ( IllegalAccessException                                  | NoSuchMethodException e) {

throw new Error (”Unexpected shape of               the         classes ” ,e );

}

catch ( SecurityException e) {

throw new Error (” Reflection                      blocked by security manager” ,e );

}

catch ( InvocationTargetException e) { Throwable cause = e . getCause (); i f ( cause instanceof RuntimeException){throw (RuntimeException) cause ;} i f ( cause instanceof Error ){throw ( Error ) cause ;}

throw new Error (”Unexpected checked exception ” , cause );

}

Often you know that either you are doing reflection right, or that if its wrong is a bug, so you want to catch checked exceptions and throw them as errors, with some special case, like for InvocationTargetException. This boring code usually have to be repeated many times in projects using reflections. With lambdas is possible to parametrize the code, and to obtain such a syntax:

return               ReflectionHelper . tryCatch (

()−<em>&gt;</em>String . class . getMethod(” toString ”). invoke (””)

);

Where the reflection method takes the body of the try, and execute it inside of a correct try−catch Your task is to complete the implementation of the method ReflectionHelper. reflection ( .. ).

You should now see the correlated tests passing.

Note well: The tryCatch method should contain the error handling behaviour shown in the handout.

<h1>3           Counting words</h1>

Here we use parallel streams to count how many times a specific word occurs into a document. This exercise require to use the variant of Stream.reduce that takes 3 arguments. See <a href="https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#reduce-U-java.util.function.BiFunction-java.util.function.BinaryOperator-">https://docs.oracle.</a>

<a href="https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#reduce-U-java.util.function.BiFunction-java.util.function.BinaryOperator-">com/javase/8/docs/api/java/util/stream/Stream.html#reduce-U-java.util.function.BiFunc</a>tion-java <a href="https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#reduce-U-java.util.function.BiFunction-java.util.function.BinaryOperator-">util.function.BinaryOperator-</a>

You can find two partially implemented versions that use parallel streams. In one we process the file line by line, in the other we process the file as as single stream of words. Your task is to complete the implementation of the methods KeywordFinder.count1(String,Path) and KeywordFinder.count2(String,Path).

In a correct implementation, they will have the same behaviour. You should now see the correlated tests passing.