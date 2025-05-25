Dictionary - A dictionary is a collection of key-value pairs, where each key is unique, and it allows fast lookups

https://www.programiz.com/online-compiler/61UJsQ5gARqTg

```c#

using System;
using System.Collections.Generic;


public class HelloWorld
{
    public static void Main(string[] args)
    {
        Dictionary<int, string> idName = new Dictionary<int, string>();
        
        //add the value
        idName.Add(1, "Priya");
        
        //access the value
        string name = idName[1];
        Console.WriteLine(name);
        
        //check if it exists
        if(idName.ContainsKey(1)){
            Console.WriteLine("Key exists");
        }
        
        //update the value 
        idName[1]="Priyanka";
        
        //Remove key
        idName.Remove(1);
        
        idName.Add(1, "Rahul");
        idName.Add(2, "Priya");
        idName.Add(3, "Naman");
        
        //loop through the dictionary
        foreach(KeyValuePair<int, string> entry in idName){
            Console.WriteLine("key:" + entry.Key+ "Value:" + entry.Value);
        }
        
        foreach(var entry in idName){
            Console.WriteLine("key:" + entry.Key+ "Value:" + entry.Value);
        }
        
        //can also loop through only key and only values
        foreach(int key in idName.Keys){
            Console.WriteLine("Key:"+key);
        }
        foreach(string val in idName.Values){
            Console.WriteLine("Value:"+val);
        }
        
        
    }
}
```