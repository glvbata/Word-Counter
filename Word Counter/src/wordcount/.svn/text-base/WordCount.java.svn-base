
package wordcount;

import java.io.File;
import java.io.FileNotFoundException;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Iterator;
import java.util.LinkedHashMap;
import java.util.List;
import java.util.Map;
import java.util.Scanner;
import java.util.Set;
import java.util.TreeMap;
import java.util.TreeSet;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * Counts the frequency of the words in a text file.
 * 
 * @author Gian Lendl V. Bata
 * @version 1.0v.
 */
public class WordCount {

  /**
   * Initial size.
   */
  private static final int INITIAL_SIZE = 0;

  /**
   * The initial top n.
   */
  private static final int INITIAL_TOP = 10;

  /**
   * A tab.
   */
  private static final String TAB = "\t";

  /**
   * A new line.
   */
  private static final String NEW_LINE = "\n";

  /**
   * The scanner to read the file.
   */
  private Scanner my_scanner;

  /**
   * The map after being sorted.
   */
  private Map<String, Integer> my_sorted_map;

  /**
   * The list where the words from the text are put into.
   */
  private List<String> my_list;

  /**
   * The hash map.
   */
  private Map<String, Integer> my_hmap;

  /**
   * The tree map.
   */
  private Map<String, Integer> my_tmap;
  
  /**
   * The map used.
   */
  private Map<String, Integer> my_map_used;

  /**
   * The string builder.
   */
  private StringBuilder my_sb;

  /**
   * The map used string representation.
   */
  private String my_map_string;

  /**
   * The top n.
   */
  private int my_top;

  /**
   * The total word count.
   */
  private int my_count;

  /**
   * The time for mapping.
   */
  private long my_time_mapping;

  /**
   * The time for getting the top n.
   */
  private long my_time_getting_top;

  /**
   * The constructor.
   */
  public WordCount() {
    my_list = new ArrayList<String>();
    my_hmap = new HashMap<String, Integer>();
    my_tmap = new TreeMap<String, Integer>();
    my_count = 0;
    my_time_mapping = 0;
    my_time_getting_top = 0;
    my_sb = new StringBuilder();
    my_top = INITIAL_TOP;
    my_map_string = "";
  }

  /**
   * Reads a file then puts all the words in a list.
   */
  public void readFile() {
    resetStat();
    String word = null;

    while (my_scanner.hasNext()) {
      word = my_scanner.next();
      my_list.add(word);
      my_count++;
    }
  }

  /**
   * Maps the list through tree map.
   */
  public void treeMapping() {

    final long previous_time = System.nanoTime();

    for (String x : my_list) {
      final String new_string = regex(x);
      final Integer count = my_tmap.get(new_string);

      if (count == null) {
        my_tmap.put(new_string, 1);
      } else {
        my_tmap.put(new_string, count + 1);
      }
    }

    final long current_time = System.nanoTime();
    my_time_mapping = current_time - previous_time;
    
    my_map_used = my_tmap;
  }

  /**
   * Maps the list through hash map.
   */
  public void hashMapping() {

    final long previous_time = System.nanoTime();

    for (String x : my_list) {
      final String new_string = regex(x);
      final Integer count = my_hmap.get(new_string);

      if (count == null) {
        my_hmap.put(new_string, 1);
      } else {
        my_hmap.put(new_string, count + 1);
      }
    }

    final long current_time = System.nanoTime();
    my_time_mapping = current_time - previous_time;
    
    my_map_used = my_hmap;
  }

  /**
   * Builds the string representation.
   */
  public void buildStringRepresentation() {
    int isize = INITIAL_SIZE;
    
    final long previous_time = System.nanoTime();
    
    my_sorted_map = sort(my_map_used);
    final Iterator<String> it = my_sorted_map.keySet().iterator();

    my_sb.append("Statistics for WordCount using " + my_map_string);
    my_sb.append("\nTotal words: " + my_count);
    my_sb.append("\nRank\tWords\tFrequency\n");

    while (isize != my_top) {
      final String key = it.next().toString();
      final String value = my_sorted_map.get(key).toString();
      isize++;

      my_sb.append("#" + isize + TAB);
      my_sb.append(key + TAB);
      my_sb.append(value + NEW_LINE);
    }

    final long current_time = System.nanoTime();
    my_time_getting_top = current_time - previous_time;

    my_sb.append("\nTime statistics:");
    my_sb.append("\nMapping\tGetting top n");
    my_sb.append(NEW_LINE + my_time_mapping + TAB + my_time_getting_top);
  }

  /**
   * Checks a string to remove unnecessary characters.
   * 
   * @param the_string the string that's getting checked.
   * @return the modified string.
   */
  public String regex(final String the_string) {
    final Pattern replace = Pattern.compile("[_\\W\\d]");
    final Matcher matcher = replace.matcher(the_string.trim());

    return matcher.replaceAll("").toLowerCase();
  }

  /**
   * Get the string representation of the map.
   * 
   * @return string representation of the map.
   */
  public String getStringRepresentation() {
    return my_sb.toString();
  }

  /**
   * Sets the file.
   * 
   * @param the_file the file.
   */
  public void setFile(final File the_file) {
    try {
      my_scanner = new Scanner(the_file);
    } catch (final FileNotFoundException e) {
      e.printStackTrace();
    }
  }

  /**
   * Sets the top highest frequencies.
   * 
   * @param the_top the top.
   */
  public void setTop(final int the_top) {
    my_top = the_top;
  }

  /**
   * Sets the map used.
   * 
   * @param the_used the used.
   */
  public void setMapUsed(final String the_used) {
    my_map_string = the_used;
  }

  /**
   * Sorts a map by value.
   * 
   * @param the_map the map
   * @return a sorted map.
   */
  public static Map<String, Integer> sort(final Map<String, Integer> the_map) {
    final Map<String, Integer> linked = new LinkedHashMap<>();
    
    linked.putAll(the_map);
    
    final List<String> keys = new ArrayList<String>(linked.keySet());
    final List<Integer> values = new ArrayList<Integer>(linked.values());

    linked.clear();

    final Set<Integer> sorted_set = new TreeSet<Integer>(values);
    final Object[] sorted_array = sorted_set.toArray();

    for (int i = sorted_array.length - 1; i > 0; i--) {
      linked.put(keys.get(values.indexOf(sorted_array[i])), (Integer) sorted_array[i]);
    }

    return linked;
  }

  /**
   * Resets statistics.
   */
  public void resetStat() {
    my_sb = new StringBuilder();
    my_count = 0;
    my_map_string = "";
    my_hmap = new HashMap<String, Integer>();
    my_tmap = new TreeMap<String, Integer>();
    my_list = new ArrayList<String>();
    my_map_used = new LinkedHashMap<String, Integer>();
    my_time_mapping = 0;
    my_time_getting_top = 0;
  }

  /**
   * Closes the file.
   */
  public void closeFile() {
    my_scanner.close();
  }
}
