# lab-sheet-11
code

FOUNDATION OF JAVA LAB SHEET
AWT AND SWING

Q1. STUDENT REGISTRATION FORM – AWT

import java.awt.*;
import java.awt.event.*;

public class Main extends Frame implements ActionListener {
    TextField name, roll, course;
    Checkbox male, female;
    CheckboxGroup gender;
    Choice semester;
    Button submit, reset;

    Main() {
        setTitle("Student Registration");
        setLayout(new GridLayout(7, 2));

        add(new Label("Student Name:"));
        name = new TextField();
        add(name);

        add(new Label("Roll Number:"));
        roll = new TextField();
        add(roll);

        add(new Label("Course:"));
        course = new TextField();
        add(course);

        add(new Label("Gender:"));
        gender = new CheckboxGroup();
        Panel p = new Panel();
        male = new Checkbox("Male", gender, true);
        female = new Checkbox("Female", gender, false);
        p.add(male);
        p.add(female);
        add(p);

        add(new Label("Semester:"));
        semester = new Choice();
        for (int i = 1; i <= 8; i++)
            semester.add("Semester " + i);
        add(semester);

        submit = new Button("Submit");
        reset = new Button("Reset");
        add(submit);
        add(reset);

        submit.addActionListener(this);
        reset.addActionListener(this);

        setSize(400, 300);
        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == submit) {
            String msg = "Name: " + name.getText() +
                "\nRoll: " + roll.getText() +
                "\nCourse: " + course.getText() +
                "\nGender: " + gender.getSelectedCheckbox().getLabel() +
                "\nSemester: " + semester.getSelectedItem();
            System.out.println(msg);
        } else {
            name.setText("");
            roll.setText("");
            course.setText("");
            gender.setSelectedCheckbox(male);
            semester.select(0);
        }
    }

    public static void main(String[] args) {
        new Main();
    }
}


Q2. SIMPLE CALCULATOR – AWT

import java.awt.*;
import java.awt.event.*;

public class Main extends Frame implements ActionListener {
    TextField t1, t2;
    Label result;
    Button add, sub, mul, div;

    Main() {
        setTitle("Calculator");
        setLayout(new GridLayout(5, 2));

        add(new Label("First Number:"));
        t1 = new TextField();
        add(t1);

        add(new Label("Second Number:"));
        t2 = new TextField();
        add(t2);

        add = new Button("Addition");
        sub = new Button("Subtraction");
        mul = new Button("Multiplication");
        div = new Button("Division");

        add(add);
        add(sub);
        add(mul);
        add(div);

        result = new Label("Result:");
        add(result);

        add.addActionListener(this);
        sub.addActionListener(this);
        mul.addActionListener(this);
        div.addActionListener(this);

        setSize(350, 250);
        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        try {
            double a = Double.parseDouble(t1.getText());
            double b = Double.parseDouble(t2.getText());
            double r;

            if (e.getSource() == add) r = a + b;
            else if (e.getSource() == sub) r = a - b;
            else if (e.getSource() == mul) r = a * b;
            else {
                if (b == 0) {
                    result.setText("Cannot divide by zero");
                    return;
                }
                r = a / b;
            }

            result.setText("Result: " + r);
        } catch (NumberFormatException ex) {
            result.setText("Enter valid numbers");
        }
    }

    public static void main(String[] args) {
        new Main();
    }
}


Q3. STUDENT LOGIN FORM – SWING

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Main extends JFrame implements ActionListener {
    JTextField user;
    JPasswordField pass;
    JButton login, reset;

    Main() {
        setTitle("Student Login");
        setLayout(new GridLayout(3, 2));

        add(new JLabel("Username:"));
        user = new JTextField();
        add(user);

        add(new JLabel("Password:"));
        pass = new JPasswordField();
        add(pass);

        login = new JButton("Login");
        reset = new JButton("Reset");
        add(login);
        add(reset);

        login.addActionListener(this);
        reset.addActionListener(this);

        setSize(350, 180);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == login) {
            String u = user.getText();
            String p = new String(pass.getPassword());

            if (u.equals("admin") && p.equals("1234"))
                JOptionPane.showMessageDialog(this, "Login Successful");
            else
                JOptionPane.showMessageDialog(this, "Invalid Username or Password");
        } else {
            user.setText("");
            pass.setText("");
        }
    }

    public static void main(String[] args) {
        new Main();
    }
}


Q4. STUDENT MARKSHEET GUI – SWING

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Main extends JFrame implements ActionListener {
    JTextField[] marks = new JTextField[5];
    String[] subjects = {"English", "Mathematics", "Java", "DBMS", "Computer Networks"};
    JButton calculate;

    Main() {
        setTitle("Student Marksheet");
        setLayout(new GridLayout(6, 2));

        for (int i = 0; i < 5; i++) {
            add(new JLabel(subjects[i]));
            marks[i] = new JTextField();
            add(marks[i]);
        }

        calculate = new JButton("Calculate Result");
        add(calculate);
        calculate.addActionListener(this);

        setSize(400, 250);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        try {
            int total = 0;
            boolean pass = true;

            for (JTextField field : marks) {
                int m = Integer.parseInt(field.getText());
                if (m < 0 || m > 100)
                    throw new NumberFormatException();

                total += m;
                if (m < 40) pass = false;
            }

            double percentage = total / 5.0;
            String grade;

            if (percentage >= 90) grade = "A+";
            else if (percentage >= 80) grade = "A";
            else if (percentage >= 70) grade = "B";
            else if (percentage >= 60) grade = "C";
            else if (percentage >= 40) grade = "D";
            else grade = "F";

            JOptionPane.showMessageDialog(this,
                "Total: " + total +
                "\nPercentage: " + percentage +
                "\nGrade: " + grade +
                "\nStatus: " + (pass ? "Pass" : "Fail"));

        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Enter valid marks (0-100)");
        }
    }

    public static void main(String[] args) {
        new Main();
    }
}


Q5. COURSE SELECTION FORM – SWING

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Main extends JFrame implements ActionListener {
    JTextField name;
    JComboBox<String> course;
    JRadioButton male, female;
    JCheckBox java, dbms, networking;
    JButton submit, reset;

    Main() {
        setTitle("Course Selection");
        setLayout(new GridLayout(6, 2));

        add(new JLabel("Student Name:"));
        name = new JTextField();
        add(name);

        add(new JLabel("Course:"));
        course = new JComboBox<>(new String[]{"BCA", "BBA", "B.Tech", "MCA"});
        add(course);

        add(new JLabel("Gender:"));
        JPanel p = new JPanel();
        male = new JRadioButton("Male", true);
        female = new JRadioButton("Female");
        ButtonGroup bg = new ButtonGroup();
        bg.add(male);
        bg.add(female);
        p.add(male);
        p.add(female);
        add(p);

        add(new JLabel("Subjects:"));
        JPanel s = new JPanel();
        java = new JCheckBox("Java");
        dbms = new JCheckBox("DBMS");
        networking = new JCheckBox("Networking");
        s.add(java);
        s.add(dbms);
        s.add(networking);
        add(s);

        submit = new JButton("Submit");
        reset = new JButton("Reset");
        add(submit);
        add(reset);

        submit.addActionListener(this);
        reset.addActionListener(this);

        setSize(450, 250);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == submit) {
            String g = male.isSelected() ? "Male" : "Female";
            String subjects = "";

            if (java.isSelected()) subjects += "Java ";
            if (dbms.isSelected()) subjects += "DBMS ";
            if (networking.isSelected()) subjects += "Networking ";

            JOptionPane.showMessageDialog(this,
                "Name: " + name.getText() +
                "\nCourse: " + course.getSelectedItem() +
                "\nGender: " + g +
                "\nSubjects: " + subjects);
        } else {
            name.setText("");
            course.setSelectedIndex(0);
            male.setSelected(true);
            java.setSelected(false);
            dbms.setSelected(false);
            networking.setSelected(false);
        }
    }

    public static void main(String[] args) {
        new Main();
    }
}


Q6. EMPLOYEE REGISTRATION FORM – AWT

import java.awt.*;
import java.awt.event.*;

public class Main extends Frame implements ActionListener {
    TextField id, name, designation, salary;
    Choice department;
    Checkbox male, female;
    CheckboxGroup gender;
    TextArea output;
    Button submit, clear;

    Main() {
        setTitle("Employee Registration");
        setLayout(new GridLayout(8, 2));

        add(new Label("Employee ID:"));
        id = new TextField();
        add(id);

        add(new Label("Name:"));
        name = new TextField();
        add(name);

        add(new Label("Department:"));
        department = new Choice();
        department.add("IT");
        department.add("HR");
        department.add("Finance");
        department.add("Sales");
        add(department);

        add(new Label("Designation:"));
        designation = new TextField();
        add(designation);

        add(new Label("Salary:"));
        salary = new TextField();
        add(salary);

        add(new Label("Gender:"));
        Panel p = new Panel();
        gender = new CheckboxGroup();
        male = new Checkbox("Male", gender, true);
        female = new Checkbox("Female", gender, false);
        p.add(male);
        p.add(female);
        add(p);

        submit = new Button("Submit");
        clear = new Button("Clear");
        add(submit);
        add(clear);

        output = new TextArea();
        add(output);

        submit.addActionListener(this);
        clear.addActionListener(this);

        setSize(450, 400);
        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == submit) {
            output.setText("Employee ID: " + id.getText() +
                "\nName: " + name.getText() +
                "\nDepartment: " + department.getSelectedItem() +
                "\nDesignation: " + designation.getText() +
                "\nSalary: " + salary.getText() +
                "\nGender: " + gender.getSelectedCheckbox().getLabel());
        } else {
            id.setText("");
            name.setText("");
            designation.setText("");
            salary.setText("");
            department.select(0);
            gender.setSelectedCheckbox(male);
            output.setText("");
        }
    }

    public static void main(String[] args) {
        new Main();
    }
}


Q7. TEMPERATURE CONVERTER – SWING

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Main extends JFrame implements ActionListener {
    JTextField temp;
    JRadioButton cToF, fToC;
    JButton convert, clear;
    JLabel result;

    Main() {
        setTitle("Temperature Converter");
        setLayout(new GridLayout(5, 2));

        add(new JLabel("Temperature:"));
        temp = new JTextField();
        add(temp);

        cToF = new JRadioButton("Celsius to Fahrenheit", true);
        fToC = new JRadioButton("Fahrenheit to Celsius");

        ButtonGroup bg = new ButtonGroup();
        bg.add(cToF);
        bg.add(fToC);

        add(cToF);
        add(fToC);

        convert = new JButton("Convert");
        clear = new JButton("Clear");
        add(convert);
        add(clear);

        result = new JLabel("Result:");
        add(result);

        convert.addActionListener(this);
        clear.addActionListener(this);

        setSize(400, 250);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == convert) {
            try {
                double t = Double.parseDouble(temp.getText());
                double ans;

                if (cToF.isSelected())
                    ans = (t * 9 / 5) + 32;
                else
                    ans = (t - 32) * 5 / 9;

                result.setText("Result: " + ans);
            } catch (NumberFormatException ex) {
                JOptionPane.showMessageDialog(this, "Enter valid temperature");
            }
        } else {
            temp.setText("");
            result.setText("Result:");
            cToF.setSelected(true);
        }
    }

    public static void main(String[] args) {
        new Main();
    }
}


Q8. SIMPLE NOTEPAD – SWING

import javax.swing.*;
import java.awt.event.*;
import java.io.*;

public class Main extends JFrame implements ActionListener {
    JTextArea area;
    JMenuItem newFile, open, save, exit;
    JFileChooser chooser;

    Main() {
        setTitle("Simple Notepad");
        area = new JTextArea();
        add(new JScrollPane(area));

        JMenuBar bar = new JMenuBar();
        JMenu file = new JMenu("File");

        newFile = new JMenuItem("New");
        open = new JMenuItem("Open");
        save = new JMenuItem("Save");
        exit = new JMenuItem("Exit");

        file.add(newFile);
        file.add(open);
        file.add(save);
        file.add(exit);
        bar.add(file);
        setJMenuBar(bar);

        newFile.addActionListener(this);
        open.addActionListener(this);
        save.addActionListener(this);
        exit.addActionListener(this);

        chooser = new JFileChooser();

        setSize(500, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        try {
            if (e.getSource() == newFile) {
                area.setText("");
            } else if (e.getSource() == open) {
                if (chooser.showOpenDialog(this) == JFileChooser.APPROVE_OPTION) {
                    BufferedReader br = new BufferedReader(
                        new FileReader(chooser.getSelectedFile()));
                    area.setText("");
                    String line;
                    while ((line = br.readLine()) != null)
                        area.append(line + "\n");
                    br.close();
                }
            } else if (e.getSource() == save) {
                if (chooser.showSaveDialog(this) == JFileChooser.APPROVE_OPTION) {
                    FileWriter fw = new FileWriter(chooser.getSelectedFile());
                    fw.write(area.getText());
                    fw.close();
                    JOptionPane.showMessageDialog(this, "File Saved Successfully");
                }
            } else if (e.getSource() == exit) {
                System.exit(0);
            }
        } catch (IOException ex) {
            JOptionPane.showMessageDialog(this, "File Error");
        }
    }

    public static void main(String[] args) {
        new Main();
    }
}


Q9. STUDENT FEEDBACK FORM – SWING

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Main extends JFrame implements ActionListener {
    JTextField name, roll, course;
    JRadioButton[] rating = new JRadioButton[5];
    JCheckBox teaching, lab, material, assignments;
    JTextArea comments;
    JButton submit, reset;

    Main() {
        setTitle("Student Feedback Form");
        setLayout(new GridLayout(7, 2));

        add(new JLabel("Student Name:"));
        name = new JTextField();
        add(name);

        add(new JLabel("Roll Number:"));
        roll = new JTextField();
        add(roll);

        add(new JLabel("Course:"));
        course = new JTextField();
        add(course);

        add(new JLabel("Rating:"));
        JPanel r = new JPanel();
        String[] ratings = {"Excellent", "Very Good", "Good", "Average", "Poor"};
        ButtonGroup bg = new ButtonGroup();

        for (int i = 0; i < 5; i++) {
            rating[i] = new JRadioButton(ratings[i]);
            bg.add(rating[i]);
            r.add(rating[i]);
        }
        rating[0].setSelected(true);
        add(r);

        add(new JLabel("Feedback:"));
        JPanel f = new JPanel();
        teaching = new JCheckBox("Teaching");
        lab = new JCheckBox("Laboratory");
        material = new JCheckBox("Course Material");
        assignments = new JCheckBox("Assignments");
        f.add(teaching);
        f.add(lab);
        f.add(material);
        f.add(assignments);
        add(f);

        add(new JLabel("Comments:"));
        comments = new JTextArea(3, 15);
        add(new JScrollPane(comments));

        submit = new JButton("Submit");
        reset = new JButton("Reset");
        add(submit);
        add(reset);

        submit.addActionListener(this);
        reset.addActionListener(this);

        setSize(650, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == submit) {
            String rate = "";
            for (JRadioButton b : rating)
                if (b.isSelected()) rate = b.getText();

            String feedback = "";
            if (teaching.isSelected()) feedback += "Teaching ";
            if (lab.isSelected()) feedback += "Laboratory ";
            if (material.isSelected()) feedback += "Course Material ";
            if (assignments.isSelected()) feedback += "Assignments ";

            JOptionPane.showMessageDialog(this,
                "Name: " + name.getText() +
                "\nRoll: " + roll.getText() +
                "\nCourse: " + course.getText() +
                "\nRating: " + rate +
                "\nFeedback: " + feedback +
                "\nComments: " + comments.getText());
        } else {
            name.setText("");
            roll.setText("");
            course.setText("");
            rating[0].setSelected(true);
            teaching.setSelected(false);
            lab.setSelected(false);
            material.setSelected(false);
            assignments.setSelected(false);
            comments.setText("");
        }
    }

    public static void main(String[] args) {
        new Main();
    }
}


Q10. MINI BANKING GUI APPLICATION – SWING

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Main extends JFrame implements ActionListener {
    JTextField account, name, balance, amount;
    JButton deposit, withdraw, check, clear;

    Main() {
        setTitle("Mini Banking Application");
        setLayout(new GridLayout(6, 2));

        add(new JLabel("Account Number:"));
        account = new JTextField();
        add(account);

        add(new JLabel("Customer Name:"));
        name = new JTextField();
        add(name);

        add(new JLabel("Current Balance:"));
        balance = new JTextField("0");
        add(balance);

        add(new JLabel("Amount:"));
        amount = new JTextField();
        add(amount);

        deposit = new JButton("Deposit");
        withdraw = new JButton("Withdraw");
        check = new JButton("Check Balance");
        clear = new JButton("Clear");

        add(deposit);
        add(withdraw);
        add(check);
        add(clear);

        deposit.addActionListener(this);
        withdraw.addActionListener(this);
        check.addActionListener(this);
        clear.addActionListener(this);

        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        try {
            double bal = Double.parseDouble(balance.getText());

            if (e.getSource() == deposit) {
                double amt = Double.parseDouble(amount.getText());
                if (amt <= 0) throw new NumberFormatException();

                bal += amt;
                balance.setText(String.valueOf(bal));
                JOptionPane.showMessageDialog(this, "Amount Deposited Successfully");

            } else if (e.getSource() == withdraw) {
                double amt = Double.parseDouble(amount.getText());
                if (amt <= 0) throw new NumberFormatException();

                if (amt <= bal) {
                    bal -= amt;
                    balance.setText(String.valueOf(bal));
                    JOptionPane.showMessageDialog(this, "Withdrawal Successful");
                } else {
                    JOptionPane.showMessageDialog(this, "Insufficient Balance");
                }

            } else if (e.getSource() == check) {
                JOptionPane.showMessageDialog(this, "Current Balance: " + bal);

            } else {
                account.setText("");
                name.setText("");
                amount.setText("");
            }

        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Enter valid positive numbers");
        }
    }

    public static void main(String[] args) {
        new Main();
    }
}
