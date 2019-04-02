Java exceptions fall into two categories, 
called checked and unchecked exceptions. 

When you call a method that throws a checked exception, 
the compiler checks that you don't ignore it. 
You must tell the compiler what you are going to do about the exception if it is ever thrown. 
For example, all subclasses of IOException are checked exceptions. 
On the other hand, 
the compiler does not require you to keep track of unchecked exceptions. 

Exceptions, such as NumberFormatException, IllegalArgumentException, and NullPointerException, 
are unchecked exceptions. More generally, 
all exceptions that belong to subclasses of RuntimeException are unchecked, 
and all other subclasses of the class Exception are checked. 

There is a second category of internal errors that are reported by throwing objects of type Error. 
One example is the OutOfMemoryError, 
which is thrown when all available memory has been used up. 
These are fatal errors that happen rarely and are beyond your control. 
They too are unchecked. 
     
Unchecked exceptions extend the class RuntimeException or Error. 

Why have two kinds of exceptions? 
A checked exception describes a problem that is likely to occur at times, 
no matter how careful you are. 
The unchecked exceptions, on the other hand, are your fault. 

For example, an unexpected end of file can be caused by forces beyond your control, 
such as a disk error or a broken network connection. 
But you are to blame for a NullPointerException, because your code was wrong when it tried to use a null reference.      
   
 
Checked exceptions are due to external circumstances that the programmer cannot prevent. 
The compiler checks that your program handles these exceptions. 
 
  
 



The compiler doesn't check whether you handle a NullPointer-Exception, because you should test your references for null before using them rather than install a handler for that exception. The compiler does insist that your program be able to handle error conditions that you cannot prevent.


Actually, those categories aren't perfect. For example, the Scanner.nextInt method throws an unchecked InputMismatchException if a user enters an input that is not an integer. A checked exception would have been more appropriate because the programmer cannot prevent users from entering incorrect input. (The designers of the Scanner class made this choice to make the class easy to use for beginning programmers.)


The majority of checked exceptions occur when you deal with input and output. That is a fertile ground for external failures beyond your control—a file might have been corrupted or removed, a network connection might be overloaded, a server might have crashed, and so on. Therefore, you will need to deal with checked exceptions principally when programming with files and streams.


You have seen how to use the Scanner class to read data from a file, by passing a FileReader object to the Scanner constructor: 
String filename = . . .;
FileReader reader = new FileReader(filename);
Scanner in = new Scanner(reader);

However, the FileReader constructor can throw a FileNotFoundException. The FileNotFoundException is a checked exception, so you need to tell the compiler what you are going to do about it. You have two choices. You can handle the exception or you can simply tell the compiler that you are aware of this exception and that you want your method to be terminated when it occurs. The method that reads input rarely knows what to do about an unexpected error, so that is usually the better option.


To declare that a method should be terminated when a checked exception occurs within it, tag the method with a throws specifier. 
public class DataSet
{
   public void read(String filename) throws FileNotFoundException
   {
      FileReader reader = new FileReader(filename);
      Scanner in = new Scanner(reader);
      . . .
   }
   . . .
}

The throws clause in turn signals the caller of your method that it may encounter a FileNotFoundException. Then the caller needs to make the same decision—handle the exception, or tell its caller that the exception may be thrown.      
   
 
Add a throws specifier to a method that can throw a checked exception. 
 
 
 
   
    
 



If your method can throw checked exceptions of different types, you separate the exception class names by commas: 
public void read (String filename)
      throws IOException, ClassNotFoundException

Always keep in mind that exception classes form an inheritance hierarchy. For example, FileNotFoundException is a subclass of IOException. Thus, if a method can throw both an IOException and a FileNotFoundException, you only tag it as throws IOException.


It sounds somehow irresponsible not to handle an exception when you know that it happened. Actually, though, it is usually best not to catch an exception if you don't know how to remedy the situation. After all, what can you do in a low-level read method? Can you tell the user? How? By sending a message to System.out? You don't know whether this method is called in a graphical program or an embedded system (such as a vending machine), where the user may never see System.out. And even if your users can see your error message, how do you know that they can understand English? Your class may be used to build an application for users in another country. If you can't tell the user, can you patch up the data and keep going? How? If you set a variable to zero, null or an empty string, that may just cause the program to break later, with much greater mystery.


Of course, some methods in the program know how to communicate with the user or take other remedial action. By allowing the exception to reach those methods, you make it possible for the exception to be processed by a competent handler. 
