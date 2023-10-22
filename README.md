# ExceptionHandling
using System;

public class CustomException : Exception
{
    public CustomException(string message) : base(message)
    {
    }
}

class Program
{
    static void Main()
    {
        int start, end;

        // Prompt the user for the start and end numbers
        Console.Write("Enter the start number: ");
        if (int.TryParse(Console.ReadLine(), out start) && start >= 1 && start <= 10)
        {
            Console.Write("Enter the end number: ");
            if (int.TryParse(Console.ReadLine(), out end) && end >= 1 && end <= 10)
            {
                for (int i = 0; i < 10; i++)
                {
                    try
                    {
                        int num = ReadNumber(start, end);
                        Console.WriteLine("Square root of the number is: " + Math.Sqrt(num));
                    }
                    catch (CustomException cx)
                    {
                        Console.WriteLine("Custom Exception: " + cx.Message);
                    }
                    catch (Exception x)
                    {
                        Console.WriteLine("General Exception: " + x.Message);
                    }
                    finally
                    {
                        Console.WriteLine("Goodbye");
                    }
                }

                Console.WriteLine($"Start number: {start}");
                Console.WriteLine($"End number: {end}");
            }
            else
            {
                Console.WriteLine("Invalid end number. Please enter a valid integer between 1 and 10.");
            }
        }
        else
        {
            Console.WriteLine("Invalid start number. Please enter a valid integer between 1 and 10.");
        }
    }

    static int ReadNumber(int start, int end)
    {
        int num;
        Console.Write($"Enter an integer between {start} and {end}: ");
        if (int.TryParse(Console.ReadLine(), out num))
        {
            if (num >= start && num <= end)
            {
                return num;
            }
            else
            {
                throw new CustomException("Invalid number");
            }
        }
        else
        {
            throw new FormatException("Invalid input. Please enter a valid integer.");
        }
    }
}
