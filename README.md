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


                         
