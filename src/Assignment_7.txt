// this is the casino slot machine game
// it uses the Triple string class and creates
// an object that produces winnings or no winnings
// depending on given probabilities of strings

import java.util.Scanner;

public class Foothill 
{
   // constant probabilities of strings
   private final static int BAR_PROB = 38;
   private final static int CHERRY_PROB = 40;
   private final static int SPACE_PROB = 7;
   private final static int SEVEN_PROB = 15;

   // main method
   public static void main(String args[]) 
   {
      // arbitrary number to continue loop
      int number = -1;
      do 
      {
         // gets user bet amount
         number = Foothill.getBet();

         // if user inputs a valid bet
         if (number > 0) 
         {
            TripleString run = Foothill.pull();
            int multiply = Foothill.getPayMultiplier(run);
            int money = number * multiply;
            Foothill.display(run, money);
         }
      } 
      while (number != 0);
   }

   public static int getBet() 
   {
      Scanner in = new Scanner(System.in);
      
      // arbitrary min and max bets, has exit value
      final int MIN_BET = 1; 
      final int MAX_BET = 50; 
      final int STOP = 0; 
      int bet = -1;

      // loops until a valid user bet is given
      do 
      {
         System.out.print("Please enter a bet between " + MIN_BET 
               + " and " + MAX_BET + " or 0 to exit: ");
            bet = in.nextInt();
         if ((bet != STOP) && !((MIN_BET <= bet)&& (bet <= MAX_BET)))
         {
            System.out.println("Invalid bet. Please try again." + "\n");
         }
         in.nextLine();
      } 
      while ((bet != STOP) && !((MIN_BET <= bet) && (bet <= MAX_BET)));
      return bet;
   }

   // picks random strings from probabilities
   private static String randString() 
   {
      int rand = (int) (Math.random() * 1000) + 1;
      if (rand <= (BAR_PROB * 10))
      {
         return "BAR";
      }
      else if (rand > (BAR_PROB * 10) && 
            rand <= ((CHERRY_PROB + BAR_PROB) * 10))
      {
         return "CHERRIES";
      }
      else if (rand > ((CHERRY_PROB + BAR_PROB) * 10) && 
            rand <= ((CHERRY_PROB + BAR_PROB + SEVEN_PROB) * 10))
      {
         return "SEVEN";
      }
      else if (rand > ((CHERRY_PROB + BAR_PROB + SEVEN_PROB) * 10) 
            && rand <= ((CHERRY_PROB + BAR_PROB 
                  + SEVEN_PROB + SPACE_PROB) * 10))
      {
         return "SPACE";
      }
      else
      {
         return "";
      }
   }

   // creates object with three strings
   public static TripleString pull() 
   {
      return new TripleString(randString(), randString(), randString());
   }

   // calculates multiplier from strings in created object
   public static int getPayMultiplier(TripleString thePull) 
   {
      if (thePull.getString1() == "CHERRIES") 
      {
         if (thePull.getString2() == "CHERRIES") 
         {
            if (thePull.getString3() == "CHERRIES") 
            {
               return 30;
            }
            else 
            {
               return 15;
            }
         } 
         else 
         {
            return 5;
         }
      } 
      else 
      {
         if (thePull.getString1().equals("BAR") 
               && thePull.getString2().equals("BAR")
               && thePull.getString3().equals("BAR")) 
         {
            return 50;
         } 
         else if (thePull.getString1().equals("SEVEN") 
               && thePull.getString2().equals("SEVEN")
               && thePull.getString3().equals("SEVEN")) 
         {
            return 100;
         } 
         else
         {
            return 0;
         }
      }
   }

   // prints the winnings after each run
   public static void display(TripleString thePull, int winnings) 
   {
      System.out.println(thePull);

      if (winnings == 0)
      {
         System.out.println("Sorry, you lose" + "\n");
      }
      else
      {
         System.out.println("WOO! YOU WON $" + winnings + "\n");
      }
   }
}

//includes constructor, set string, get string, and printed output
class TripleString
{
   private String string1;
   private String string2;
   private String string3;

   // irrelevant constants
   public static final String DEFAULT_STRING = " (undefined) ";
   public static final int MIN_LEN = 1;
   public static final int MAX_LEN = 50;

   // constructor with three parameters
   public TripleString(String str1, String str2, String str3)
   {
      if(!setString1(str1))
      {
         string1 = DEFAULT_STRING;
      }
      if(!setString2(str2))
      {
         string2 = DEFAULT_STRING;
      }
      if(!setString3(str3))
      {
         string3 = DEFAULT_STRING;
      }
   }

   // constructor with no parameters
   public TripleString()
   {
      string1 = DEFAULT_STRING;
      string2 = DEFAULT_STRING;
      string3 = DEFAULT_STRING;
   }

   // checks if each string meets criteria
   private static boolean validString(String str)
   {
      if(str != null && str.length() >= MIN_LEN 
            && str.length() <= MAX_LEN)
      {
         return true;
      }
      else
      {
         return false;
      }
   }

   // sets string1 to new string if valid
   public boolean setString1(String str1) 
   {
      if(!validString(str1))
      {
         return false;
      }
      else
      {
         this.string1 = str1;
         return true;
      }         
   }

   // sets string2 to new string if valid
   public boolean setString2(String str2) 
   {
      if(!validString(str2))
      {
         return false;

      }
      else
      {
         this.string2 = str2;
         return true;
      }         
   }

   // sets string3 to new string if valid
   public boolean setString3(String str3) 
   {
      if(!validString(str3))
      {
         return false;
      }
      else
      {
         this.string3 = str3;
         return true;
      }         
   }

   // return string1
   public String getString1() 
   {
      return string1;
   }

   // return string2
   public String getString2() 
   {
      return string2;
   }

   // return string3
   public String getString3() 
   {
      return string3;
   }

   // formatted output for each run
   public String toString()
   {
      String string = "string1: " + string1 + ", string2: " 
            + string2 + ", string3: " + string3;
      return string;
   }
}
/*
\\\\\\\\\\\\\\\\\\ PASTED OUTPUT ////////////////////////

BAR BAR BAR in groups 8 and 40

CHERRIES CHERRIES CHERRIES in groups 14, 21, 22, 29, 35, 
37, 38, 41, 43


Please enter a bet between [0 and 50] or 0 to exit: -1
Invalid bet. Please try again.

Please enter a bet between [0 and 50] or 0 to exit: 51
Invalid bet. Please try again.

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: BAR, string3: CHERRIES
WOO! YOU WON $10

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: SPACE, string3: BAR
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: BAR, string3: CHERRIES
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: SPACE, string3: CHERRIES
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: SEVEN, string3: SPACE
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: BAR, string3: BAR
WOO! YOU WON $100

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: CHERRIES, string3: SEVEN
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: SEVEN, string2: BAR, string3: CHERRIES
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: BAR, string3: CHERRIES
WOO! YOU WON $10

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: CHERRIES, string3: BAR
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: BAR, string3: BAR
WOO! YOU WON $10

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: CHERRIES, string3: CHERRIES
WOO! YOU WON $60

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: CHERRIES, string3: SPACE
WOO! YOU WON $30

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: CHERRIES, string3: BAR
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: SPACE, string3: BAR
WOO! YOU WON $10

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: BAR, string3: SEVEN
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: SEVEN, string2: BAR, string3: SEVEN
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: SPACE, string2: BAR, string3: SPACE
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: CHERRIES, string3: CHERRIES
WOO! YOU WON $60

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: CHERRIES, string3: CHERRIES
WOO! YOU WON $60

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: SPACE, string3: BAR
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: CHERRIES, string3: CHERRIES
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: BAR, string3: BAR
WOO! YOU WON $10

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: SEVEN, string3: BAR
WOO! YOU WON $10

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: BAR, string3: SEVEN
WOO! YOU WON $10

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: CHERRIES, string3: BAR
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: CHERRIES, string3: CHERRIES
WOO! YOU WON $60

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: CHERRIES, string3: BAR
WOO! YOU WON $30

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: CHERRIES, string3: SEVEN
WOO! YOU WON $30

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: SPACE, string2: BAR, string3: CHERRIES
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: SEVEN, string2: BAR, string3: CHERRIES
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: SPACE, string3: CHERRIES
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: CHERRIES, string3: CHERRIES
WOO! YOU WON $60

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: CHERRIES, string3: CHERRIES
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: CHERRIES, string3: CHERRIES
WOO! YOU WON $60

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: CHERRIES, string3: CHERRIES
WOO! YOU WON $60

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: BAR, string3: CHERRIES
WOO! YOU WON $10

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: BAR, string3: BAR
WOO! YOU WON $100

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: CHERRIES, string3: CHERRIES
WOO! YOU WON $60

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: SPACE, string2: SEVEN, string3: CHERRIES
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: CHERRIES, string3: CHERRIES
WOO! YOU WON $60

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: BAR, string3: CHERRIES
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: SPACE, string2: BAR, string3: BAR
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: BAR, string3: SEVEN
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: BAR, string3: CHERRIES
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: CHERRIES, string3: SPACE
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: SEVEN, string3: SEVEN
WOO! YOU WON $10

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: CHERRIES, string2: BAR, string3: BAR
WOO! YOU WON $10

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: BAR, string2: SPACE, string3: BAR
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 2
string1: SEVEN, string2: SEVEN, string3: BAR
Sorry, you lose

Please enter a bet between [0 and 50] or 0 to exit: 0

*/