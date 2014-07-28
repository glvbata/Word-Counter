
package gui;

import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.File;

import javax.swing.BorderFactory;
import javax.swing.ButtonGroup;
import javax.swing.JButton;
import javax.swing.JFileChooser;
import javax.swing.JFrame;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JRadioButton;
import javax.swing.JTextArea;
import javax.swing.JTextField;

import wordcount.WordCount;

/**
 * The GUI for the WordCount Class.
 * 
 * @author Gian Lendl V. Bata
 * @version 1.0v.
 */
@SuppressWarnings("serial")
public class Window extends JFrame {

  /**
   * The width.
   */
  public static final int HEIGHT = 200;

  /**
   * The Height.
   */
  public static final int WIDTH = 50;

  /**
   * The scale.
   */
  public static final int SCALE = 3;

  /**
   * The title.
   */
  public static final String TITLE = "Word Counter";

  /**
   * The default top n.
   */
  public static final int DEFAULT_TOP = 10;

  /**
   * The frame.
   */
  private final JFrame my_frame;

  /**
   * The file text field.
   */
  private final JTextField my_file_textfield;

  /**
   * The top text field.
   */
  private final JTextField my_top_textfield;

  /**
   * The map label.
   */
  private final JTextArea my_map_textarea;

  /**
   * The open button.
   */
  private JButton my_open_button;

  /**
   * The top n button.
   */
  private JButton my_top_button;

  /**
   * The top n.
   */
  private int my_top_n;

  /**
   * The word count object.
   */
  private final WordCount my_w;

  /**
   * The hash radio button.
   */
  private JRadioButton my_hash_radio;

  /**
   * The constructor.
   */
  public Window() {
    super();
    my_w = new WordCount();
    my_frame = new JFrame();
    my_top_n = DEFAULT_TOP;

    my_file_textfield = new JTextField("");
    my_top_textfield = new JTextField("");
    my_map_textarea = new JTextArea("");

    my_file_textfield.setPreferredSize(new Dimension(100, 20));
    my_top_textfield.setPreferredSize(new Dimension(30, 20));

    setPreferredSize(new Dimension(WIDTH * SCALE, HEIGHT * SCALE));
  }

  /**
   * Runs the program.
   */
  public void run() {
    layoutPanels();
    layoutFrame();
  }

  /**
   * Layout the panels.
   */
  public void layoutPanels() {
    final JPanel first_panel = new JPanel();
    final JPanel second_panel = new JPanel();
    final JPanel third_panel = new JPanel();
    final ButtonGroup radio_group = new ButtonGroup();
    final JButton map_button = new JButton("Map It");
    final JRadioButton tree_radio = new JRadioButton("Tree Map");
    my_open_button = new JButton("Open File");
    my_top_button = new JButton("Set Top n");
    my_hash_radio = new JRadioButton("Hash Map");

    radio_group.add(tree_radio);
    radio_group.add(my_hash_radio);
    my_hash_radio.doClick();

    first_panel.add(my_file_textfield);
    first_panel.add(my_open_button);
    first_panel.add(my_top_textfield);
    first_panel.add(my_top_button);

    second_panel.setBorder(BorderFactory.createLineBorder(Color.black));
    second_panel.setBackground(Color.WHITE);
    second_panel.setPreferredSize(new Dimension(200, 500));
    second_panel.add(my_map_textarea);

    third_panel.add(my_hash_radio);
    third_panel.add(tree_radio);
    third_panel.add(map_button);

    final ButtonHandler button_handler = new ButtonHandler();
    my_open_button.addActionListener(button_handler);
    my_top_button.addActionListener(button_handler);
    map_button.addActionListener(button_handler);

    my_frame.add(first_panel, BorderLayout.NORTH);
    my_frame.add(second_panel, BorderLayout.CENTER);
    my_frame.add(third_panel, BorderLayout.SOUTH);
    my_frame.add(new JPanel(), BorderLayout.WEST);
    my_frame.add(new JPanel(), BorderLayout.EAST);
  }

  /**
   * Layouts the frame.
   */
  public void layoutFrame() {
    my_frame.setResizable(false);
    my_frame.setTitle(TITLE);

    my_frame.pack();
    my_frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    my_frame.setLocationRelativeTo(null);
    my_frame.setVisible(true);
    my_frame.setLayout(new BorderLayout());
  }

  /**
   * Gets the file via JFileChooser.
   */
  public void getFile() {
    final JFileChooser jfile_chooser = new JFileChooser("C:/");

    final int chooser = jfile_chooser.showOpenDialog(null);
    final File file = jfile_chooser.getSelectedFile();

    if (chooser == JFileChooser.APPROVE_OPTION) {

      my_file_textfield.setText(file.getName());
      my_w.setFile(file);

    } else if (chooser != JFileChooser.APPROVE_OPTION) {
      JOptionPane.showMessageDialog(null, "You have canceled choosing a file.");
    }
  }

  /**
   * Sets the top n of words with the most frequencies.
   */
  public void setTop() {
    try {
      if (my_top_textfield == null) {
        my_top_n = DEFAULT_TOP;
      } else {
        my_top_n = Integer.parseInt(my_top_textfield.getText());
      }

      my_w.setTop(my_top_n);
    } catch (final Exception e) {
      JOptionPane.showMessageDialog(null,
        "Make sure to type in a number before pressing the top n button.");
    }
  }

  /**
   * Maps the list of words.
   */
  public void mapFile() {
    try {
      my_w.readFile();

      if (my_hash_radio.isSelected()) {
        my_w.hashMapping();
        my_w.setMapUsed("HashMap");
      } else {
        my_w.treeMapping();
        my_w.setMapUsed("TreeMap");
      }

      my_w.buildStringRepresentation();
      my_map_textarea.setText(my_w.getStringRepresentation());
      my_w.closeFile();

    } catch (final Exception e) {
      JOptionPane.showMessageDialog(null, "Open a proper text file before each mapping.");
    }

  }

  /**
   * The button handler.
   * 
   * @author Gian Lendl V. Bata
   * @version 1.0v.
   */
  public class ButtonHandler implements ActionListener {

    /**
     * This method runs when one of the buttons is clicked.
     * 
     * @param the_event the event.
     */
    public void actionPerformed(final ActionEvent the_event) {

      if (the_event.getSource() == my_open_button) {
        getFile();
      } else if (the_event.getSource() == my_top_button) {
        setTop();
      } else {
        mapFile();
      }
    }
  }

}
