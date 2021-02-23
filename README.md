# DetectTheEmailAddresses
Detect the Email Addresses C# Hackerrak



using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Text.RegularExpressions;
using System.Threading.Tasks;

namespace DetectTheEmailAddresses
{
    public class Solution
    {
        public static void Main(string[] args)
        {
            int N = Int32.Parse(Console.ReadLine());

            string words = "";

            for (int i = 0; i < N; i++)
            {
                words += " " + Console.ReadLine();
            }

            //string regex = @"\w+@[\w.-]+|\{(?:\w+, *)+\w+\}@[\w.-]+";
            string regex = @"[\w+-]+(?:\.[\w+-]+)*@[\w+-]+(?:\.[\w+-]+)*(?:\.[a-zA-Z]{2,4})";

            MatchCollection t = Regex.Matches(words, regex);

            HashSet<string> emails = new HashSet<string>();

            for (int i = 0; i < t.Count; i++)
            {
                string res = t[i].ToString();

                // Capture potential ends of sentences
                if (res.EndsWith("."))
                {
                    res = res.Substring(0, res.Length - 1);
                }

                emails.Add(res);
            }

            string[] arr = new string[emails.Count];

            arr = emails.Where(r => char.IsUpper(r[0])).OrderBy(r => r).Concat(emails.Where(r => char.IsLower(r[0])).OrderBy(r => r)).ToArray();
            
            string output = "";

            for (int i = 0; i < arr.Length; i++)
            {
                if (i < arr.Length - 1)
                    output += arr[i] + ";";
                else
                    output += arr[i];
            }

            Console.WriteLine(output);
        }
    }
}
