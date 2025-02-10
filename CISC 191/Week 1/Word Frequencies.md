## Word Frequencies Activity

1)
![Word Frequencies drawio](https://github.com/user-attachments/assets/fd818f67-a492-4aa6-b9cf-e4a202bb0a6b)

2) In a frequency analysis of a website, I’d first extract all the text from the page, then break it into individual words. I’d remove some of the basic words like "the" or "and" that don’t really tell you much. Next, I’d count how many times each remaining word shows up. Finally, I’d look at the most frequently-occurring words to get a sense of the main ideas or topics on the site.
3) At first I wasn't getting the right output and I really struggled trying to find the issue in my code. It was leaving out the last two lines and only outputting:
"hey 1
Hi 2
Mark 2"
I solved this by changing "if (wordsProcessed[j].equalsIgnoreCase(currWord))" to: "if (wordsProcessed[j].equals(currWord))" when checking for words that have already been processed.
4) https://youtube.com/shorts/IOraSpIeMKI?feature=share
5)
```java
import java.util.Scanner;

class WordFrequency {

    // calculate the frequency of a word in the list
    public static int getWordFrequency(String[] wordsList, int listSize, String currWord) {
        int count = 0;
        // loop through the list to count occurrences of the word
        for (int i = 0; i < listSize; i++) {
            if (wordsList[i].equalsIgnoreCase(currWord)) {  // Case-insensitive comparison
                count++;
            }
        }
        return count;
    }

    public static void main(String[] args) {
        Scanner keyboard = new Scanner(System.in);

        // read line of words
        System.out.println("Enter the words (space-separated):");
        String input = keyboard.nextLine();  // Read the full line
        
        // split input into an array of words
        String[] wordsList = input.split("\\s+");  // Split by whitespace

        // create array to track which words have already been processed (case-insensitive)
        String[] wordsProcessed = new String[wordsList.length];
        int processedIndex = 0;  // track the index of words already processed

        // loop through words and calculate frequency for each unique word
        for (int i = 0; i < wordsList.length; i++) {
            String currWord = wordsList[i];
            boolean alreadyProcessed = false;

            // check if word has already been processed (case-insensitive)
            for (int j = 0; j < processedIndex; j++) {
                if (wordsProcessed[j].equals(currWord)) {
                    alreadyProcessed = true;
                    break;
                }
            }

            // if word hasn't been processed yet, calculate and print its frequency
            if (!alreadyProcessed) {
                int frequency = getWordFrequency(wordsList, wordsList.length, currWord);
                System.out.println(currWord + " " + frequency);

                // mark word as processed (store it in the wordsProcessed array)
                wordsProcessed[processedIndex++] = currWord;
            }
        }

        keyboard.close();
    }
}
   ```
