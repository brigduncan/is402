# is402

/*  Name: Brigham Duncan
    Date: September 13, 2016
    Class: Information Systems 402
    Description:  This program prompts the user to enter the number of teams competing in an olympic soccer tournament.  After
    entering the number of teams competing, the user will enter the name of the teams and how many points they won.  The results 
    of the tournament will be displayed at the end.
*/


    public class Team //parent class
    {
        public string name;
        public int wins;
        public int loss;
    }
    public class SoccerTeam : Team //child class
    {
        public int draw;
        public int goalsFor;
        public int goalsAgainst;
        public int differential;
        public int points;

        public SoccerTeam (string sName, int iPoints) //constructor
        {
            this.name = sName;
            this.points = iPoints;
        }
    }

    public class game
    {
        public int homeScore;
        public int visitorScore;
    }

    class Program
    {
        static string UppercaseFirst(string s) // Function that capitalizes the first letter of the teams entered.
        {
            // Check for empty string.
            if (string.IsNullOrEmpty(s))
            {
                return string.Empty;
            }
            // Return char and concat substring.
            return char.ToUpper(s[0]) + s.Substring(1);
        }

        static void Main(string[] args) 
        {
            int numberOfTeams = 0;
            int teamCounter = 1;
            
            while (teamCounter<2)     //Exemption handling.  Makes sure a string isn't entered where an integer is expected.
            {
                try //Checking for an integer.
                {
                    Console.Write("How many teams? ");
                    numberOfTeams = Convert.ToInt32(Console.ReadLine());
                    teamCounter = 2; 
                }
                catch //The output when an integer isn't entered.
                {
                    Console.Write("Invalid Entry.  Please try again.\n");
                }
            }

            List<SoccerTeam> teamName = new List<SoccerTeam>(); //Creates list of teams.
            Console.Write("\n");

          int tPoints = 0;
          int pointCounter = 1;
          for (int counter  = 1; counter <= numberOfTeams; counter++)
           {
               Console.Write("\n");

               Console.Write("Enter Team " + counter + "'s name: ");
               string tName = UppercaseFirst(Console.ReadLine());

               while (pointCounter < 2) //Exemption handling.  Makes sure a string isn't entered where an integer is expected.
               {
                   try //Checking for an integer.
                   {
                       Console.Write("\nEnter " + tName + "'s points: ");
                       
                       tPoints = Convert.ToInt32(Console.ReadLine());
                       pointCounter = 2;
                   }
                   catch //The output when an integer isn't entered.
                   {
                       Console.Write("Invalid Entry.  Please try again.\n");
                   }
                     
               }
               pointCounter = 0;

               SoccerTeam newTeam = new SoccerTeam(tName, tPoints); //This creates a new soccer team.

               teamName.Add(newTeam); //Adds the new team to the list of soccer teams.
           }


           //Start of the ordered table of teams.
           List<SoccerTeam> sortedTeams = teamName.OrderByDescending(team => team.points).ToList(); //Linq statement that orders the teams by amount of points they scored.

           Console.Write("\n\nHere is the sorted list:\n\n");
           Console.Write("Position\tName\t\t\tPoints\n--------\t----\t\t\t------\n");

           //I used tabs for the labeling of the table and used padding for the actual output.

           int i = 0;
           foreach (SoccerTeam team in teamName) //Output displayed in the table.
           {
               Console.WriteLine(Convert.ToString(i + 1).PadRight(16, ' ') + sortedTeams[i].name.PadRight(24, ' ') + sortedTeams[i].points);
               i++;
           }

           Console.ReadLine(); //To keep the program open when it is executed in the console.
        }
    }

    
}

 
