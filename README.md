import java.io.File;//For the file
import java.io.FileNotFoundException;//for file not found
import java.io.PrintWriter;//for print writer
import java.util.Arrays;//for array
import java.util.Scanner;//for scanner

public class SongReport 
{
   public static void main(String[] args) //main class method
      {
       int NumberOfFiles = 2;//for number of files
       for(int i=1;i<=NumberOfFiles;i++)
         {
      }
       Scanner sc = new Scanner(System.in);//for scanner
       File file = new File("Songs.csv"); //This reads data from the name file
       Scanner reader;
       String line="";

       int maxArtistPossible = 1000;//for max artists

       String artists[] = new String[maxArtistPossible];//max artists
       int artistsCount[] = new int[maxArtistPossible];//for artists counts

       int currentIndex=0;//current index
       for(int i=0;i<artistsCount.length;i++)
       {
           artistsCount[i] = 0;//reset count to 0
       }
       int songRecordCount=0;//for song count record

       try 
       {
           reader = new Scanner(file);//scanner
           while(reader.hasNextLine())
           {
               songRecordCount++;
               //to read line
               line = reader.nextLine();
               String columns[] = line.split(",(?=(?:[^\"]*\"[^\"]*\")*[^\"]*$)");

               //Artist will be at position 2
               String tmpArtist = columns[2];

               //the following remove the quotes from the line
               tmpArtist = tmpArtist.replaceAll("\"", "");
               for(String art : tmpArtist.split(","))
               {
                   boolean found = false;//boolean method
                   for(int i=0;i<currentIndex;i++)
                   {
                       if(art.equalsIgnoreCase(artists[i]))
                       {
                           artistsCount[i]++;
                           found = true;
                           break;
                       }
                   }
                   if(!found)
                   {
                       artists[currentIndex] = art;
                       artistsCount[currentIndex]=1;
                       currentIndex++;
                   }
               }
           }
       } 
       catch (FileNotFoundException e) 
       {
           System.out.println("file not found");
       }

      
       System.out.println("Total song loaded : "+songRecordCount);
       System.out.println("Total unique artist count is : "+currentIndex);
       System.out.printf("%-25s%s\n","Artist","Occurence count");
       for(int i=0;i<currentIndex;i++){
           System.out.printf("%-25s%s\n",artists[i],artistsCount[i]);
       }
       sc.close();
   }


}
