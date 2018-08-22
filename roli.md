``` c-sharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text.RegularExpressions;

namespace Roli
{
    class Program
    {
        static void Main(string[] args)
        {
            //KEY IS NOT A NUMBER or not?
            //key -> ID
            //VALUE -> NAME -> PARTICIPANT
            //•	{id} #{eventName} @{participant1} @{participant2} … @{participantN}
            string patternEvent = @"(?<id>\d+) #(?<name>[A-Za-z0-9\-\']+) (?<members>.+)";
            string patternMember = @"@[A-Za-z0-9\-\']+";

            string line = Console.ReadLine();
            Dictionary<int, string> eventNames = new Dictionary<int, string>();
            Dictionary<int, List<String>> eventMembers = new Dictionary<int, List<string>>();
            while (line != "Time for Code")
            {
                Match matchEvent = Regex.Match(line, patternEvent);
                if (matchEvent.Success)
                {
                    int id = int.Parse(matchEvent.Groups["id"].Value);
                    string name = matchEvent.Groups["name"].Value;
                    string members = matchEvent.Groups["members"].Value;

                    List<string> membersList = new List<string>();
                    foreach (Match member in Regex.Matches(members, patternMember))
                    {
                        if (member.Success)
                        {
                            membersList.Add(member.Value);
                        }
                    }
                    if (eventNames.ContainsKey(id) == false)
                    {
                        eventNames.Add(id, name);
                        eventMembers.Add(id, membersList);
                    }
                    else
                    {
                        if (eventNames[id] == name)
                        {
                            eventMembers[id].AddRange(membersList);
                        }
                    }


                }
                    line = Console.ReadLine();
            }

            foreach (var @event in eventMembers.OrderByDescending(x=>x.Value.Count).ThenBy(x=>eventNames[x.Key]))
            {
                Console.WriteLine($"{eventNames[@event.Key]} - {@event.Value.Distinct().ToArray().Length}");
                foreach (var member in @event.Value.Distinct().OrderBy(x=>x))
                {
                    Console.WriteLine(member);
                }
            }

        }
    }
}
```