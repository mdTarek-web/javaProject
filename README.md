import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class NumberOperations {
    private JFrame frame;
    private JTextField n1, n2, n3, result;
    private JButton max, min, avg, clr;

    public NumberOperations() {
        frame = new JFrame("Number Operations");
        frame.setLayout(new FlowLayout());

        // Text fields
        n1 = new JTextField(5);
        n2 = new JTextField(5);
        n3 = new JTextField(5);
        result = new JTextField(10);
        result.setEditable(false);

        // Buttons
        max = new JButton("Max");
        min = new JButton("Min");
        avg = new JButton("Avg");
        clr = new JButton("Clear");

        // Add components to frame
        frame.add(new JLabel("n1:"));
        frame.add(n1);
        frame.add(new JLabel("n2:"));
        frame.add(n2);
        frame.add(new JLabel("n3:"));
        frame.add(n3);
        frame.add(max);
        frame.add(min);
        frame.add(avg);
        frame.add(clr);
        frame.add(new JLabel("Result:"));
        frame.add(result);

        // Event handling for buttons
        max.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                double num1 = Double.parseDouble(n1.getText());
                double num2 = Double.parseDouble(n2.getText());
                double num3 = Double.parseDouble(n3.getText());
                double maxValue = Math.max(num1, Math.max(num2, num3));
                result.setText(String.valueOf(maxValue));
            }
        });

        min.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                double num1 = Double.parseDouble(n1.getText());
                double num2 = Double.parseDouble(n2.getText());
                double num3 = Double.parseDouble(n3.getText());
                double minValue = Math.min(num1, Math.min(num2, num3));
                result.setText(String.valueOf(minValue));
            }
        });

        avg.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                double num1 = Double.parseDouble(n1.getText());
                double num2 = Double.parseDouble(n2.getText());
                double num3 = Double.parseDouble(n3.getText());
                double average = (num1 + num2 + num3) / 3;
                result.setText(String.valueOf(average));
            }
        });

        clr.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                n1.setText("");
                n2.setText("");
                n3.setText("");
                result.setText("");
            }
        });

        // Set frame properties
        frame.setSize(300, 250);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }

    public static void main(String[] args) {
        new NumberOperations();
    }
}







(a) Suppose that you are required to write a Java programfor implementingaGUIusinganylayout.GUI initiallycontainsasinglebuttonnamedADD. ADDbuttondynamicallyaddsanewbuttontotheframewhenit isclicked.Eachnewbuttonshouldhaveaunique label too(suchasb1, b2,b3...).Notethat thebuttonsor labelsshouldnotoverlap.Nowdothefollowingtasktodemonstrateyourskill:
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class DynamicButtonGUI {
    private JFrame frame;
    private JPanel panel;
    private JButton addButton;
    private int buttonCount = 1;

    public DynamicButtonGUI() {
        frame = new JFrame("Dynamic Button Add");
        panel = new JPanel();
        panel.setLayout(new FlowLayout());

        // Initialize the "ADD" button
        addButton = new JButton("ADD");
        addButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                // Dynamically add a new button with a unique label
                JButton newButton = new JButton("b" + buttonCount);
                panel.add(newButton);  // Add the new button to the panel
                panel.revalidate();  // Revalidate the layout
                panel.repaint();     // Repaint the panel to show the new button
                buttonCount++;       // Increment the button count for the next unique label
            }
        });

        panel.add(addButton);
        frame.add(panel);

        // Set frame properties
        frame.setSize(400, 300);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }

    public static void main(String[] args) {
        new DynamicButtonGUI();
    }
}                          






Asfaq,afirst-yearprogrammingstudent, learnedhowtofindthehighestnumberfromanarrayusingtheJava program.Excitedwithhisnewfoundknowledge,hestartedtowonder ifhecouldconcurrentlydothesamefor multiplearrays.OneofhisseniorstoldhimtouseThreadwhichfacilitatestorunmultipletasksconcurrently. Basedontheidea,inordertohelpAsfaq,yourtaskisto-writeaJavaprogramthatcanfindthehighestnumbersfrom4integerarraysconcurrentlyandnext,compute themaximumofthesehighestnumbersandprintthemaximumnumber.Considerthearraysas {3,1,-5,10},{-2,6,7,8,0},{12,-6,4,2,1},{10,5,-9,18,7}.
public class ConcurrentMaxFinder {

    // Class to handle finding the maximum in an array
    static class MaxFinder extends Thread {
        private int[] array;
        private int maxValue;

        public MaxFinder(int[] array) {
            this.array = array;
        }

        @Override
        public void run() {
            maxValue = findMax(array);
        }

        public int getMaxValue() {
            return maxValue;
        }

        private int findMax(int[] array) {
            int max = array[0];
            for (int num : array) {
                if (num > max) {
                    max = num;
                }
            }
            return max;
        }
    }

    public static void main(String[] args) throws InterruptedException {
        // The four integer arrays
        int[] array1 = {3, 1, -5, 10};
        int[] array2 = {-2, 6, 7, 8, 0};
        int[] array3 = {12, -6, 4, 2, 1};
        int[] array4 = {10, 5, -9, 18, 7};

        // Create thread objects
        MaxFinder maxFinder1 = new MaxFinder(array1);
        MaxFinder maxFinder2 = new MaxFinder(array2);
        MaxFinder maxFinder3 = new MaxFinder(array3);
        MaxFinder maxFinder4 = new MaxFinder(array4);

        // Start all threads
        maxFinder1.start();
        maxFinder2.start();
        maxFinder3.start();
        maxFinder4.start();

        // Wait for all threads to finish
        maxFinder1.join();
        maxFinder2.join();
        maxFinder3.join();
        maxFinder4.join();

        // Find the maximum value among the highest values from each array
        int maxOfMax = Math.max(maxFinder1.getMaxValue(), Math.max(maxFinder2.getMaxValue(),
                Math.max(maxFinder3.getMaxValue(), maxFinder4.getMaxValue())));

        // Print the result
        System.out.println("The maximum of the highest numbers from the arrays is: " + maxOfMax);
    }
}




)Suppose thatyouaregivena text filenamed“input.txt”withrandomtexts.Nowyouhavetocheckhow manyconsonantsareinthefileandwriteittoanothertextfilenamed“output.txt”.Forexample,iftheinputfile containsthefollowingtext-“Don’tbeupset”,youshouldwrite“7”intheoutputfile.Boththefilesshouldbe inthe“src”directory.Now,writeaprograminJavatoperformthistask
import java.io.*;

public class ConsonantCounter {
    public static void main(String[] args) {
        // File paths for input and output files
        String inputFilePath = "src/input.txt";
        String outputFilePath = "src/output.txt";

        try {
            // Read the content from the input file
            BufferedReader reader = new BufferedReader(new FileReader(inputFilePath));
            StringBuilder text = new StringBuilder();
            String line;

            // Read each line of the file
            while ((line = reader.readLine()) != null) {
                text.append(line).append(" "); // Append each line and space between lines
            }
            reader.close(); // Close the reader

            // Count consonants in the text
            int consonantCount = countConsonants(text.toString());

            // Write the consonant count to the output file
            BufferedWriter writer = new BufferedWriter(new FileWriter(outputFilePath));
            writer.write(String.valueOf(consonantCount));
            writer.close(); // Close the writer

            System.out.println("Consonant count written to output.txt: " + consonantCount);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // Method to count consonants in a given text
    public static int countConsonants(String text) {
        int count = 0;
        // Convert the text to lowercase for easier matching
        text = text.toLowerCase();

        // Loop through each character of the text
        for (int i = 0; i < text.length(); i++) {
            char c = text.charAt(i);
            // Check if the character is a consonant (i.e., an alphabetic character that's not a vowel)
            if (Character.isLetter(c) && !isVowel(c)) {
                count++;
            }
        }
        return count;
    }

    // Helper method to check if a character is a vowel
    public static boolean isVowel(char c) {
        return c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u';
    }
}



                         
