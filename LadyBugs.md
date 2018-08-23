```csharp
using System;
using System.Linq;

namespace LadyBugs
{
    class Program
    {
        static void Main(string[] args)
        {
            int size = int.Parse(Console.ReadLine());
            if (size == 0)
            {
                return;
            }
            int[] field = new int[size];

            int[] indices = Console.ReadLine()
                .Split()
                .Select(int.Parse)
                .ToArray();

            foreach (var index in indices)
            {
                if (index < 0 || size <= index)
                {
                    continue;
                }
                field[index] = 1;
            }
           

            string command = Console.ReadLine();
            while (command != "end")
            {
                var tokens = command.Split().ToArray();
                int index = int.Parse(tokens[0]);
                string direction = tokens[1];
                int len = int.Parse(tokens[2]);
                if (direction == "left")
                {
                    len *= -1;
                }
                if (index < field.Length && index >= 0)
                {
                    if (field[index] != 0)
                    {
                        if (len != 0)
                        {
                            Fly(field, index, len);
                            field[index] = 0;
                        }
                    }
                }
                command = Console.ReadLine();
            }

            Console.WriteLine(string.Join(" ", field));

        }

        public static void Fly(int[] field, int index, int len)
        {
            if (index + len >= field.Length || index + len < 0)
            {
                return;
            }

            int target = field[index + len];
            if (target == 1)
            {
                Fly(field, index + len, len);
            }
            else
            {
                field[index + len] = 1;
            }
        }
    }
}
```