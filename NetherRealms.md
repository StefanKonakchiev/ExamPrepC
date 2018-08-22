
``` javascript
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text.RegularExpressions;

namespace NetherRealms2
{
    class Program
    {
        static void Main(string[] args)
        {
            string patternHP = @"[^0-9+\-*\/.]";
            string patternDM = @"(-)?\d+(\.\d+)*";

            string[] demons = Console.ReadLine().Split(new char[] { ',',' '}, StringSplitOptions.RemoveEmptyEntries).ToArray();
            List<string> sortedDemons = new List<string>();

           
            
            foreach (var demon in demons)
            {
                double totalHP = 0;
                foreach (Match match in Regex.Matches(demon, patternHP))
                {
                    if (match.Success)
                    {
                        totalHP += match.Value[0];
                    }
                }
                double totalDM = 0;
                //Console.WriteLine(totalHP);
                foreach (Match number in Regex.Matches(demon, patternDM))
                {
                    if (number.Success)
                    {
                        totalDM += double.Parse(number.Value);
                    }
                }

                var multiplication = demon.Where(x => x == '*').ToArray();
                var division = demon.Where(x => x == '/').ToArray();

                totalDM = totalDM * (Math.Pow(2, multiplication.Length));
                totalDM = totalDM / (Math.Pow(2, division.Length));
                //Console.WriteLine(totalDM);

                string result = $"{demon} - {totalHP} health, {totalDM:f2} damage";

                sortedDemons.Add(result);
            }

            sortedDemons = sortedDemons.OrderBy(x => x).ToList();
            

            foreach (var demon in sortedDemons)
            {
                Console.WriteLine(demon);
            }


        }
    }
}

```