```csharp
using System;

namespace CharityMarathon
{
    class Program
    {
        static void Main(string[] args)
        {
            long days = int.Parse(Console.ReadLine());
            long runnersCount = int.Parse(Console.ReadLine());
            long averageLaps = int.Parse(Console.ReadLine());
            long length = int.Parse(Console.ReadLine());
            long capacity = int.Parse(Console.ReadLine());
            double moneyPerKm = double.Parse(Console.ReadLine());

            var maximumRunners = days * capacity;
            if (runnersCount > maximumRunners)
            {
                runnersCount = maximumRunners;
            }

            var totalMeters = runnersCount*averageLaps*length;
            double totalKm = totalMeters / 1000.0;

            double totalMoney = totalKm * moneyPerKm;

            Console.WriteLine($"Money raised: {totalMoney:f2}");

        }
    }
}
```