# logg-out-logg-in-system
want to add a email verification system in my existing code
import javax.swing.*;
import java.awt.event.*;
import java.util.HashMap;



public class karan_prasad4 extends JFrame implements ActionListener {
    private static HashMap<String, String> userDatabase = new HashMap<>();
    private static HashMap<String, String> loggedInUsers = new HashMap<>();

    private JTextField usernameField;
    private JPasswordField passwordField;
    private JButton loginButton;
    private JButton logoutButton;
    private JButton createButton;

    public karan_prasad4 () {
        setTitle("Login System");
        setSize(300, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JPanel panel = new JPanel();
        add(panel);
        placeComponents(panel);

        setVisible(true);
    }

    private void placeComponents(JPanel panel) {
        panel.setLayout(null);

        JLabel userLabel = new JLabel("Username");
        userLabel.setBounds(10, 20, 80, 25);
        panel.add(userLabel);

        usernameField = new JTextField(20);
        usernameField.setBounds(100, 20, 160, 25);
        panel.add(usernameField);

        JLabel passwordLabel = new JLabel("Password");
        passwordLabel.setBounds(10, 50, 80, 25);
        panel.add(passwordLabel);

        passwordField = new JPasswordField(20);
        passwordField.setBounds(100, 50, 160, 25);
        panel.add(passwordField);

        loginButton = new JButton("Login");
        loginButton.setBounds(10, 80, 80, 25);
        loginButton.addActionListener(this);
        panel.add(loginButton);

        logoutButton = new JButton("Logout");
        logoutButton.setBounds(100, 80, 80, 25);
        logoutButton.addActionListener(this);
        panel.add(logoutButton);

        createButton = new JButton("Create Account");
        createButton.setBounds(10, 110, 150, 25);
        createButton.addActionListener(this);
        panel.add(createButton);

        logoutButton.setEnabled(false);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == loginButton) {
            String username = usernameField.getText();
            String password = new String(passwordField.getPassword());

            if (userDatabase.containsKey(username) && userDatabase.get(username).equals(password)) {
                loggedInUsers.put(username, password);
                JOptionPane.showMessageDialog(this, "Welcome, " + username + "!");
                loginButton.setEnabled(false);
                logoutButton.setEnabled(true);
                createButton.setEnabled(false);
            } else {
                JOptionPane.showMessageDialog(this, "Invalid username or password.");
            }

        } else if (e.getSource() == logoutButton) {
            String username = usernameField.getText();
            loggedInUsers.remove(username);
            JOptionPane.showMessageDialog(this, "Logged out successfully.");
            loginButton.setEnabled(true);
            logoutButton.setEnabled(false);
            createButton.setEnabled(true);

        } else if (e.getSource() == createButton) {
            String newUsername = usernameField.getText();
            String newPassword = new String(passwordField.getPassword());

            if (!newUsername.isEmpty() && !newPassword.isEmpty()) {
                userDatabase.put(newUsername, newPassword);
                JOptionPane.showMessageDialog(this, "Account created successfully.");
            } else {
                JOptionPane.showMessageDialog(this, "Please enter a valid username and password.");
            }
        }
    }

    public static void main(String[] args) {
        new karan_prasad4 ();
    }
}
