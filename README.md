# test

Revision pour mes tests

package algorithmes;

import java.util.Arrays;
import java.util.Comparator;
import java.util.List;
import java.util.stream.Collectors;

public class ArabeToRomainNumbers {

    enum RomanNumeral {
        I(1), IV(4), V(5), IX(9), X(10),
        XL(40), L(50), XC(90), C(100),
        CD(400), D(500), CM(900), M(1000);

        private int value;

        RomanNumeral(int value) {
            this.value = value;
        }

        public int getValue() {
            return value;
        }

        public static List<RomanNumeral> getReverseSortedValues() {
            return Arrays.stream(values())
                    .sorted(Comparator.comparing((RomanNumeral e) -> e.value).reversed())
                    .collect(Collectors.toList());
        }
    }
    /**
     * Main method
     *
     * @param args
     */
    public static void main(String[] args) {
        System.out.println("Arabic to romain : " + arabicToRoman(1983));
        System.out.println("Romain to Arabic : " + romanToArabic("MMXVIII"));
    }

    public static String arabicToRoman(int number) {
        if ((number <= 0) || (number > 4000)) {
            throw new IllegalArgumentException(number + " is not in range (0,4000]");
        }

        List<RomanNumeral> romanNumerals = RomanNumeral.getReverseSortedValues();

        int i = 0;
        StringBuilder sb = new StringBuilder();

        while ((number > 0) && (i < romanNumerals.size())) {
            RomanNumeral currentSymbol = romanNumerals.get(i);
            if (currentSymbol.getValue() <= number) {
                sb.append(currentSymbol.name());
                number -= currentSymbol.getValue();
            } else {
                i++;
            }
        }

        return sb.toString();
    }

    public static int romanToArabic(String input) {
        String romanNumeral = input.toUpperCase();
        int result = 0;

        List<RomanNumeral> romanNumerals = RomanNumeral.getReverseSortedValues();

        int i = 0;

        while ((romanNumeral.length() > 0) && (i < romanNumerals.size())) {
            RomanNumeral symbol = romanNumerals.get(i);
            if (romanNumeral.startsWith(symbol.name())) {
                result += symbol.getValue();
                romanNumeral = romanNumeral.substring(symbol.name().length());
            } else {
                i++;
            }
        }

        if (romanNumeral.length() > 0) {
            throw new IllegalArgumentException(input + " cannot be converted to a Roman Numeral");
        }

        return result;
    }
}

package algorithmes;

// Do not modify Change
class Change {
    long coin2 = 0;
    long bill5 = 0;
    long bill10 = 0;
}

package algorithmes;

public class ChangeMoney {
    public static void main(String[] args) {
        // Arrays to perform tests
        long[] tests = { 1, 17, 16, 6, 13 };

        for (long s : tests) {
            Change m = Solution.optimalChange(s);
            Solution.printResult(m, s);
        }
    }
}

package algorithmes;

import java.util.Random;

/**
 * Implémentez la méthode closestToZero pour renvoyer l'entier du tableau ints le plus proche de zéro.
 * <p>
 * S'il y a deux entiers tout aussi proches de zéro, considérez l'entier positif comme étant le plus proche de zéro (par
 * exemple si ints contient -5 et 5, retournez 5).
 * <p>
 * Si ints est null ou vide, retournez 0 (zero).
 * <p>
 * Données : les entiers dans ints ont des valeurs allant de -2147483647 à 2147483647.
 */

public class ClosestToZero {

    public static void main(String[] args) {
        int size = 2000;// test 1k, 10k, 100k, 1Million
        int[] arrayInt = new int[size];
        Random s = new Random();
        for (int i = 0; i < size; i++) {
            arrayInt [i] = s.nextInt(); // String.valueOf(s.nextInt());
        }
        int i = closestToZero(arrayInt);
        System.out.println("Closest to zero is : " + i);
    }
    static int closestToZero(int[] ints) {

        if (ints.length == 0 || ints == null) {
            return 0;
        }

        int T;
        int min = Integer.MAX_VALUE;
        /* Search the temperature of minimum absolute valueReads */
        for (int i = 0; i < ints.length; i++) {
            T = ints[i];
            if (Math.abs(T) < Math.abs(min) || (T == -min && T > 0)) {
                min = T;
            }
        }
        return min;
    }

}


package algorithmes;

import java.util.*;

/**
 * check if an array contains a certain value ?
 *
 */

public class ExistsInArrays {

    /*
     *
     * Nombre dans un tableau (tutoriel)
     *
     * Le but de cet exercice est de vérifier la présence d’un nombre dans un tableau.
     *
     * Spécifications : Les éléments sont des nombres entiers classés du plus petit au plus grand
     *
     * Le tableau peut contenir jusqu’à 1 million d’éléments
     *
     * Le tableau n’est jamais null
     *
     * Implémentez la méthode boolean A.exists(int[]ints, int k) afin qu’elle retourne true si k est présent dans ints,
     * sinon la méthode devra retourner false.
     *
     * Important : Essayez de privilégier le temps d'exécution.
     *
     * Exemple : int[] ints = {-9, 14, 37, 102}; A.exists(ints, 102) retourne true A.exists(ints, 36) retourne false
     *
     *
     * test if : La solution fonctionne avec un 'petit' tableau (200 pts) - Résolution de problèmes La solution
     * fonctionne avec un tableau vide (50 pts) - Fiabilité La solution fonctionne en un temps raisonnable avec 1
     * million d'items (700 pts) - Résolution de problèmes La solution utilise l'api J2SE pour effectuer la recherche
     * dichotomique. (200 pts) - Connaissance du langage
     *
     * search an array of size 5, 1k, 10k. 100K, 1 millons
     *
     */

    /**
     * LIST
     * <p>
     * this method is inefficient. Pushing the array to another collection requires spin through all elements to read
     * them in before doing anything with the collection type.
     */
    public static boolean useList(Integer[] arr, Integer targetValue) {
        return Arrays.asList(arr).contains(targetValue);
    }

    /**
     * SET
     * <p>
     * hashset can do it in O(1)
     */
    public static boolean useSet(Integer[] arr, Integer targetValue) {
        Set<Integer> set = new HashSet<Integer>(Arrays.asList(arr));
        return set.contains(targetValue);
    }

    /**
     * LOOP
     * <p>
     * using a simple loop method is more efficient than using any collection
     */
    public static boolean useLoop(Integer[] arr, Integer targetValue) {
        for (Integer s : arr) {
            if (s.equals(targetValue))
                return true;
        }
        return false;
    }

    static boolean exists(int[] ints, int k) {
        for (int s : ints) {
            if (s == k)
                return true;
        }
        return false;
    }

    /**
     * Arrays.binarySearch()
     * <p>
     * Use if array is SORTED
     * <p>
     * a sorted list or tree can do it in O(log(n))
     */
    public static boolean useArraysBinarySearch(Integer[] arr, Integer targetValue) {
        int a = Arrays.binarySearch(arr, targetValue);
        return a > 0;
    }

    /**
     * Main METHOD
     */
    public static void main(String[] args) {


        // Use a larger array
        int size = 1000000;// test 1k, 10k, 100k, 1Million
        Integer arrInt[] = new Integer[size];
        Random s = new Random();
        for (int i = 0; i < size; i++) {
            arrInt[i] = s.nextInt(); // String.valueOf(s.nextInt());
        }

        // use list
        long startTime = System.nanoTime();
        int value = arrInt[800000];
        boolean b2 = useList(arrInt, value);
        long endTime = System.nanoTime();
        long duration = endTime - startTime;
        System.out.println("useList:  " + b2 + " " + duration);

        // use set
        startTime = System.nanoTime();
        boolean b1 = useSet(arrInt, value);
        endTime = System.nanoTime();
        duration = endTime - startTime;
        System.out.println("useSet:  " + b1 + " " + duration);

        // use loop
        startTime = System.nanoTime();
        boolean b3 = useLoop(arrInt, value);
        endTime = System.nanoTime();
        duration = endTime - startTime;
        System.out.println("useLoop:  " + b3 + " " + duration);

        // use Arrays.binarySearch()
        List<Integer> list = Arrays.asList(arrInt);
        Collections.sort(list);
        Integer[] sortedArray = (Integer[]) list.toArray();
        startTime = System.nanoTime();
        boolean b4 = useArraysBinarySearch(sortedArray, value);
        endTime = System.nanoTime();
        duration = endTime - startTime;
        System.out.println("useArrayBinary:  " + b4 + " " + duration);

        List<Integer> arrayIntegerList = Arrays.asList(arrInt);
        startTime = System.nanoTime();
        boolean contains = arrayIntegerList.contains(value);
        endTime = System.nanoTime();
        duration = endTime - startTime;
        System.out.println("list.contains:  " + contains + " " + duration);

        Set<Integer> set = new HashSet<Integer>(arrayIntegerList);
        startTime = System.nanoTime();
        boolean contains1 = set.contains(value);
        endTime = System.nanoTime();
        duration = endTime - startTime;
        System.out.println("set.contains1:  " + contains1 + " " + duration);

    }

}

package algorithmes;

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

/**
 * La suite de algorithme.Fibonacci est une suite d'entier dont la valeur de chaque terme est égale à la somme des valeurs des deux
 * termes précédents. C'est donc une suite récurrente.
 * <p>
 * on commence par 1 et 1 -> 1+1 =2 -> 1+2=3 -> 2+3=5 -> 3+5=8 -> 5+8=13 ...-> 21 -> 34 -> 55
 * <p>
 * on n'étudie pas les nombres de algorithme.Fibonacci pour des valeurs négatives de n suite observé fréquement dans la nature en
 * botanique, dans des varaition tel quel que les fluctuation de la bourse ou la beauté humaine
 * <p>
 * WAY 1 : fonction récursive Ce n'est cependant pas une façon judicieuse de calculer la suite de algorithme.Fibonacci, car on
 * calcule de nombreuses fois les mêmes valeurs . Le temps de calcul s'avère exponentiel
 * <p>
 * WAY 2 : moyen bien plus efficace de calculer la suite de algorithme.Fibonacci consiste à calculer simultanément deux valeurs
 * consécutives de la suite
 *
 */
public class Fibonacci {
    /**
     * Main Method
     */
    public static void main(String[] args) {

        System.out.println("result for 4 and UP :" + fibbWithClosetNumber(4, closest.UP));
        System.out.println("result for 4 and DOWN :" + fibbWithClosetNumber(4, closest.DOWN));
        fibonacci1(args);
    }

    /**
     * Suite de fibonacci & la valeur la plus proche selon la direction donnée
     */
    public static Integer fibbWithClosetNumber(Integer number, closest en) {
        int fib = 1;
        int termePrec1 = 2;
        int termePrec2 = 1;

        System.out.println("Les " + number + " premiers éléments de la suite de algorithme.Fibonacci sont : ");

        List<Integer> resultList = new ArrayList<>();
        Integer result = 0;

        for (int i = 1; i <= number; i++) {

            if (i == 2) {
                fib = 2;
            }

            if (i > 2) {
                fib = termePrec1 + termePrec2;
                termePrec2 = termePrec1;
                termePrec1 = fib;
            }

            resultList.add(fib);

        }

        // retourne l'element le plus p^roche
        if (closest.DOWN.equals(en)) {
            for (Integer e : resultList) {
                if (e == number - 1)
                    result = e;
            }

        } else {
            for (Integer e : resultList) {
                if (e == number + 1)
                    result = e;
            }
        }

        return result;
    }

    /**
     * x0=0 , X1=1, xn=xn-2+xn-1
     *
     * @param args
     */
    public static void fibonacci1(String[] args) {

        int nbElement;

        int fib = 1;
        int terme_prec1 = 2;
        int terme_prec2 = 1;

        @SuppressWarnings("resource")
        Scanner sc = new Scanner(System.in);
        System.out.println("Entrez le nombre de algorithme.Fibonacci a calculer ? : ");
        nbElement = sc.nextInt();
        System.out.println("Les " + nbElement + " premiers éléments de la suite de algorithme.Fibonacci sont : ");

        for (int i = 1; i <= nbElement; i++) {

            if (i == 2) {
                fib = 2;
            }

            if (i > 2) {
                fib = terme_prec1 + terme_prec2;
                terme_prec2 = terme_prec1;
                terme_prec1 = fib;
            }

            System.out.print(fib + ";");
        }

    }

}

/**
 * Closest ENUM with instance UP and DOWN
 */
enum closest {

    UP,

    DOWN;

}

***************

package algorithmes;

/**
 * FIZZBUZZ
 * <p>
 * A program that prints the numbers from 1 to 100.
 * <ul>
 * <li>But for multiples of 3 print "Fizz" instead of the number</li>
 * <li>and for the multiples of 5 print"Buzz".</li>
 * <li>For numbers which are multiples of both three and five print "algorithme.FizzBuzz"</li>
 * </ul>
 */
public class FizzBuzz {
    static String newLine = System.getProperty("line.separator");

    public static void main(String[] args) {
        fizzBuzz0();
        fizzBuzz1();
        // fizzBuzz2();
        // fizzBuzz3();
    }

    /**
     * no good way
     */
    public static void fizzBuzz0() {
        System.out.println(newLine + "fizzBuzz0() :");
        for (int i = 1; i <= 100; i++) {
            String test = "";
            test += (i % 3) == 0 ? "fizz" : "";
            test += (i % 5) == 0 ? "buzz" : "";
            System.out.println(!test.isEmpty() ? test : i);
        }
    }

    /**
     * StringBuilder seems a faster approach than += in this case
     */
    public static void fizzBuzz1() {
        // StringBuilder builder = new StringBuilder(1000); //do not care about the capacity, It automatically grows to
        // accomodate whatever is necessary. You can play with it to improve performance, but it's still asymptotically
        // linear.
        StringBuilder builder = new StringBuilder("fizzBuzz1() with StringBuilder : ");

        for (int i = 1; i <= 100; i++) {
            final int length = builder.length();

            if (i % 3 == 0)
                builder.append("Fizz");
            if (i % 5 == 0)
                builder.append("Buzz");
            if (length == builder.length())
                builder.append(i);

            builder.append(',');
        }
        System.out.println(newLine + builder);
    }

    /**
     * The % 15 version is simpler and easier to read. This version neatly
     */
    public static void fizzBuzz2() {
        String buzz = "buzz";
        String fizz = "fizz";

        for (int i = 1; i <= 100; i++) {
            if (i % 15 == 0) {
                System.out.println(buzz + fizz + " " + i);
            } else if (i % 3 == 0) {
                System.out.println(buzz + " " + i);
            } else if (i % 5 == 0) {
                System.out.println(fizz + " " + i);
            }
        }
    }

    /**
     * succint way
     */
    public static void fizzBuzz3() {
        for (int i = 0; i < 100; i++) {
            System.out.println(newLine + "fizzBuzz1() :"
                    + ((i % 3 == 0 || i % 5 == 0) ? ((i % 3) == 0 ? "fizz" : "") + ((i % 5) == 0 ? "buzz" : "") : i));
        }
    }
}
***********

package algorithmes;

import java.util.ArrayList;
import java.util.List;

public class GroupeMatchs {

    /**
     * problème : je dispose d'une liste de joueurs d'un jeu à deux joueurs (échecs, ping-pong, etc.), et je veux créer
     * une liste de matches, de telle sorte que chaque joueur joue contre tous les autres joueurs une seule fois.
     */
    public static List<String> MatchTwoPlayerOfListPlayer(ArrayList<String> joueurs) {

        List<String> matches = new ArrayList<>();
        /* s'il n'y a qu'un seul joueur, on n'organise aucun match */
        if (joueurs == null || joueurs.size() < 2) {
            return matches;
        }
        /* on enleve le dernier joueur de la liste, et on demande les matchs sans lui */
        String dernierJoueur = joueurs.remove(joueurs.size() - 1);
        // $matches = MatchTwoPlayerOfListPlayer($joueurs);

        /* on rajoute un match entre lui et tous les autres joue!urs */
        for (String autreJoueurs : joueurs) {
            // $matches[] = array($autre_joueur, $dernier_joueur);
            matches.add(autreJoueurs + " vs " + dernierJoueur);
        }

        /* on le remet dans la liste des joueurs, et on renvoie la liste des matchs */
        // array_push($joueurs, $dernier_joueur);
        return matches;
    }

    /**
     * Main method
     *
     * @param args
     */
    public static void main(String[] args) {
        System.out.println("Matches du groupe : ");
        ArrayList<String> equipes = new ArrayList<>();
        equipes.add("Espagne");
        equipes.add("Portugal");
        equipes.add("Tunisie");
        equipes.add("Maroc");
        List<String> matchs = MatchTwoPlayerOfListPlayer(equipes);
        for(String match : matchs) {
            System.out.println(match);
        }
    }
}
********
package algorithmes;

import readers.ReadFile;

import java.util.*;

/**
 * How to find highest repeated word from a file
 * <p>
 * Java program to find the duplicate word which has occurred maximum number of times in a file.
 */
public class HighestRepeatingWord {
    /**
     * Main method
     */
    public static void main(String args[]) {
        Map<String, Integer> wordMap = ReadFile.buildWordMap("C:/temp/words.txt");
        List<Map.Entry<String, Integer>> list = sortByValueInDecreasingOrder(wordMap);
        System.out.println("List of repeated word from file and their count");
        for (Map.Entry<String, Integer> entry : list) {
            if (entry.getValue() > 1) {
                System.out.println(entry.getKey() + " => " + entry.getValue());
            }
        }
    }


    /**
     * Sort a given Map
     *
     * @param wordMap
     * @return
     */
    public static List<Map.Entry<String, Integer>> sortByValueInDecreasingOrder(Map<String, Integer> wordMap) {
        Set<Map.Entry<String, Integer>> entries = wordMap.entrySet();
        List<Map.Entry<String, Integer>> list = new ArrayList<>(entries);
        Collections.sort(list, new Comparator<Map.Entry<String, Integer>>() {
            @Override
            public int compare(Map.Entry<String, Integer> o1, Map.Entry<String, Integer> o2) {
                return (o2.getValue()).compareTo(o1.getValue());
            }
        });
        return list;
    }

}

**********
package algorithmes;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;
import java.util.stream.Collectors;

/**
 * Ajout d'un élement a une liste triée , quelque soit le sens du tri et retourner une nouvelle liste triée intégrant
 * l'élément
 */
public class InsertInSortedList {

    /**
     * Main Method
     */
    public static void main(String[] args) {

        List<Integer> sortedListASC = new ArrayList<>(Arrays.asList(1, 3, 5, 7));
        List<Integer> sortedListDESC = sortedListASC.stream().sorted(Collections.reverseOrder())
                .collect(Collectors.toList());

        try {
            System.out.println("sorted List ASC: " + sortedListASC);
            System.out.println("insertAndSort ASC: " + insertAndSort(4, sortedListASC));
            System.out.println("\n");
            System.out.println("sorted List DESC: " + sortedListDESC);
            System.out.println("insertAndSort DESC: " + insertAndSort(4, sortedListDESC));
        } catch (MyException e) {
            System.out.println(e.getMessage());
        }
    }

    /**
     * Inset and Sort IN MANUAL WAY
     */
    public static List<Integer> insertAndSort(Integer num, List<Integer> list) throws MyException {

        List<Integer> result = new ArrayList<>();

        if (num == null) {
            throw new MyException("la valleur a ajoutée est null");
        } else if (list == null || list.isEmpty()) {
            throw new MyException("la liste est null ou vide");
        } else {

            int firstElement = list.get(0);
            int lastElement = list.get(list.size() - 1);
            boolean flagNotAlredyAdded = true; // flag if num already added

            if (firstElement <= lastElement) {
                // list ASC
                for (Integer element : list) {
                    if (flagNotAlredyAdded && num < element) {
                        result.add(num);
                        result.add(element);
                        flagNotAlredyAdded = false;
                    } else {
                        result.add(element);
                    }
                }
            } else {
                // list DESC
                for (Integer element : list) {
                    if (flagNotAlredyAdded && num > element) {
                        result.add(num);
                        result.add(element);
                        flagNotAlredyAdded = false;
                    } else {
                        result.add(element);
                    }
                }
            }
        }
        return result;
    }

}

/**
 * Exeption Class
 *
 */
class MyException extends Exception {

    private static final long serialVersionUID = 1L;

    public MyException(String message) {
        System.out.println(message);
    }

}

**********
package algorithmes;

import java.util.*;

/**
 * MinMax
 * <p>
 * Chercher le plus grand et le plus petit élément Vous disposez d'une liste d'entiers positifs, et vous voulez trouver
 * le plus grand de la liste.
 * <p>
 * N comparaisons : une par élément | compléxité linéraire : O(N) l'occupation mémoire de notre algorithme est constante
 * (on note aussi O(1)
 */
public class MaxOfIntegerList {
    /**
     * Main method
     */
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5, 5, 5, 6, 6, 7, 8, 9, 9));

        long lStartTime = System.nanoTime();
        System.out.println("maxOfIntegerListElement : " + maxOfIntegerListElement(list));
        mesurer(lStartTime);

        lStartTime = System.nanoTime();
        System.out.println("maxOfIntegerListElementJava8 : " + maxOfIntegerListElementJava8(list));
        mesurer(lStartTime);

        lStartTime = System.nanoTime();
        System.out.println("minOfIntegerListJava8 : " + minOfIntegerListJava8(list));
        mesurer(lStartTime);

    }

    public static void mesurer(long startTime) {
        //end
        long endTime = System.nanoTime();

        //time elapsed
        long output = endTime - startTime;

        System.out.println("Elapsed time in milliseconds: " + output/1000000);
    }

    /**
     * @param list
     * @return
     */
    public static Integer maxOfIntegerListElement(List<Integer> list) {

        if (list != null & !list.isEmpty()) {
            Integer maxActuel = list.get(0);
            for (Integer element : list) {
                if (element > maxActuel) {
                    maxActuel = element;
                }
            }
            return maxActuel;
        }
        return null;
    }

    /**
     * @param list
     * @return
     */
    public static Integer maxOfIntegerListElementJava8(List<Integer> list) {

        /*
         * Integer currenMaxValue = 0; list.stream().forEach((element) -> { if (element > currenMaxValue) {
         * currenMaxValue = element; } }); return currenMaxValue;
         */
        Optional<Integer> max = list.stream().sorted((e1, e2) -> e2.compareTo(e1)).findFirst();
        return max.isPresent() ? max.get() : null;

    }

    /**
     * @param list
     * @return
     */
    public static Integer minOfIntegerListJava8(List<Integer> list) {

        Optional<Integer> max = list.stream().sorted((e1, e2) -> e1.compareTo(e2)).findFirst();
        return max.isPresent() ? max.get() : null;
    }
}
**********
package algorithmes;

public class MissingNumberInArray {
    public static void main(String[] args) {

        // given input
        int[] input = { 1, 1, 2, 3, 5, 5, 7, 9, 9, 9 };

        // let's create another array with same length
        // by default all index will contain zero
        // default value for int variable

        int[] register = new int[input.length];

        // now let's iterate over given array to
        // mark all present numbers in our register
        // array

        for (int i : input) {
            register[i] = 1;
        }

        // now, let's print all the absentees
        System.out.println("missing numbers in given array");

        for (int i = 1; i < register.length; i++) {
            if (register[i] == 0) {
                System.out.println(i);
            }
        }
    }
}
*********
package algorithmes;

import java.util.LinkedList;
import java.util.List;

public class PrimeNumbers {

    public static void main(String[] args) {

        List<Integer> integers = primeNumbersBruteForce(20);
        for(Integer i : integers)
        System.out.print(i + " ; ");
    }

    public static List<Integer> primeNumbersBruteForce(int n) {
        List<Integer> primeNumbers = new LinkedList<>();
        if (n >= 2) {
            primeNumbers.add(2);
        }
        for (int i = 3; i <= n; i += 2) {
            if (isPrimeBruteForce(i)) {
                primeNumbers.add(i);
            }
        }
        return primeNumbers;
    }
    private static boolean isPrimeBruteForce(int number) {
        for (int i = 2; i < number/2; i++) {
            if (number % i == 0) {
                return false;
            }
        }
        return true;
    }
}
**********
package algorithmes;

public class RecursiveFactorielle {

    /**
     * Main method
     *
     * @param args
     */
    public static void main(String[] args) {
        System.out.println("Calcul factorielle 5 : " + fact(5));
    }

    /**
     * Calcul factorielle
     */
    public static int fact(int n) {
        if (n == 0)
            return 1;
        return (n == 1) ? 1 : n * fact(n - 1);

    }

}
**********
package algorithmes;

import java.util.*;
import java.util.stream.Collectors;

public class RemoveDoublonOfList {

    public static void main(String[] args)
    {
        // input list with duplicates
        List<Integer> list = new ArrayList<>(Arrays.asList(1, 10, 1, 2, 2, 3, 10, 3, 3, 4, 5, 5));
        // Print the Arraylist
        System.out.println("ArrayList with duplicates: " + list);

        // Construct a new list from the set constucted from elements of the original list
        List<Integer> newList = list.stream().distinct().collect(Collectors.toList());

        // Print the ArrayList with duplicates removed
        System.out.println("ArrayList with duplicates removed: " + newList);
    }

    // Function to remove duplicates from an ArrayList
    public static <T> ArrayList<T> removeDuplicates(ArrayList<T> list) {
        Set<T> set = new LinkedHashSet<>();
        set.addAll(list);
        list.clear();
        list.addAll(set);
        return list;
    }

    // Function to remove duplicates from an ArrayList
    public static <T> ArrayList<T> removeDuplicates1(ArrayList<T> list) {
        // Create a new ArrayList
        ArrayList<T> newList = new ArrayList<T>();
        // Traverse through the first list
        for (T element : list) {
            // If this element is not present in newList then add it
            if (!newList.contains(element)) {
                newList.add(element);
            }
        }
        // return the new list
        return newList;
    }
}
*************
package algorithmes;

/**
 * Reverse digits of an integer.
 * <ul>
 * <li>Example1: x = 123, return 321
 * <li>Example2: x = -123, return -321
 * </ul>
 */
public class ReverseInteger {

    public static void main(String[] args) {
        System.out.println("x = 123 | reverse x = " + reverse(123));
        System.out.println("x = -123 | reverse x = " + reverse(-123));

        System.out.println("x = 123 | reverse x = " + reverse2(123));
        System.out.println("x = -123 | reverse x = " + reverse2(-123));
    }

    /**
     * Efficient Approach
     */
    public static int reverse(int x) {
        // flag marks if x is negative
        boolean flag = false;
        if (x < 0) {
            x = 0 - x;
            flag = true;
        }

        int res = 0;
        int p = x;

        while (p > 0) {
            int mod = p % 10;
            p = p / 10;
            res = res * 10 + mod;
        }

        if (flag) {
            res = 0 - res;
        }

        return res;
    }

    /**
     * Succinct solution no necessary to check whether the parameter is positive or negative. For instance, -11/10 = -1;
     * -11%10 = -1.
     */
    public static int reverse2(int x) {
        int res = 0;
        while (x != 0) {
            res = (res * 10) + (x % 10);
            x = x / 10;
        }
        return res;
    }

}
***********
package algorithmes;

import readers.ReadKeyword;

import java.util.Collections;
import java.util.LinkedList;
import java.util.ListIterator;

/**
 * exemple montrant comment utiliser une liste chaînée pour afficher à l’envers une suite de chaînes lues au clavier
 */
public class ReverseListOfWords {
    public static void main(String args[]) {
        LinkedList<String> linkedList = new LinkedList<String>();
        /* on ajoute a la liste tous les mots lus au clavier */
        String[] array = ReadKeyword.read().split(" ");
        Collections.addAll(linkedList, array);
        System.out.println("Liste des mots a linkedList'endroit :");

        ListIterator<String> iter = linkedList.listIterator();
        while (iter.hasNext()) {
            System.out.print(iter.next() + " ");
        }

        System.out.println("\n Liste des mots a linkedList'envers :");
        iter = linkedList.listIterator(linkedList.size()); // iterateur en fin de liste
        while (iter.hasPrevious())
            System.out.print(iter.previous() + " ");
        System.out.println();
    }
}
***********
package algorithmes;

public class ReverseString {


    public static void main(String[] args) {
        System.out.println("reverseWithStringBulder(\"HELLO WORLD\") : " + reverseWithStringBulder("HELLO WORLD"));
        System.out.println("reverse (\"VOITURE BMW\") : " + reverseWithoutStringBulder("VOITURE BMW"));
    }

    /**
     * Reserve String With StringBuilder.reverse()
     *
     * @param s
     *            La chaine a renverse.
     * @return la chaine renversee.
     */
    public static String reverseWithStringBulder(final String s) {
        if (s == null) {
            return null;
        }
        return new StringBuilder(s).reverse().toString();
    }

    /**
     * Reserve String Without StringBuilder.reverse()
     *
     * @param s
     *            La chaine a renverse.
     * @return la chaine renversee.
     */
    public static String reverseWithoutStringBulder(final String s) {

        if (s == null) {
            return null;
        }

        final char chaineArray[] = s.toCharArray();
        final StringBuilder s2 = new StringBuilder();
        for (final char c : chaineArray) {
            s2.insert(0, c);
        }
        return s2.toString();
    }
}
*************
package algorithmes;

import java.util.Arrays;

public class RotateArray {

    /**
     * Main method
     *
     * @param args
     */
    public static void main(String[] args) {

        int[] arr = { 1, 2, 3, 4, 5, 6, 7 };
        System.out.println("(length=7, order=3) : " + Arrays.toString(rotate(arr, 3)));

        int[] arr2 = { 1, 2, 3, 4, 5, 6 };
        System.out.println("(length=6, order=2) : " + Arrays.toString(rotate2(arr2, 2)));

    }

    /**
     * solution is like a bubble sort. tri à bulle the time is O(n*k).
     *
     */
    public static int[] rotate(int[] arr, int order) {
        if (arr == null || order < 0) {
            throw new IllegalArgumentException("Illegal argument!");
        }

        for (int i = 0; i < order; i++) {
            for (int j = arr.length - 1; j > 0; j--) {
                int temp = arr[j];
                arr[j] = arr[j - 1];
                arr[j - 1] = temp;
            }
        }
        return arr;
    }

    /**
     * Solution Reversal
     * do this in O(1) space and in O(n) time
     *
     * 1. Divide the array two parts: 1,2,3,4 and 5, 6
     * 2. Rotate first part: 4,3,2,1,5,6
     * 3. Rotate second part: 4,3,2,1,6,5
     * 4. Rotate the whole array: 5,6,1,2,3,4
     */
    public static int[] rotate2(int[] arr, int order) {
        if (arr == null || arr.length==0 || order < 0) {
            throw new IllegalArgumentException("Illegal argument!");
        }
        if(order == arr.length){
            return arr;
        }
        order = order % arr.length;
        //length of first part
        int a = arr.length - order;
        reverse(arr, 0, a-1);
        reverse(arr, a, arr.length-1);
        reverse(arr, 0, arr.length-1);
        return arr;
    }

    public static void reverse(int[] arr, int left, int right){
        if(arr == null || arr.length == 1)
            return;
        while(left < right){
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }

}
************
package algorithmes;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class SearchFileDirectory {

    public static void main(String[] args) {
        find();
        walk();
    }

    private static void find() {
        try (
                Stream<Path> stream = Files.find(Paths.get("C:\\Intel"), 5,
                        (path, attr) -> path.getFileName().toString().equals("IntelGFX.log"))) {
            System.out.println(stream.findAny().isPresent());
        } catch (
                IOException e) {
            e.printStackTrace();
        }
    }

    private static void walk() {
        Path startWalk = Paths.get("C:\\Intel");
        int depth = 5;
        try (Stream<Path> stream1 = Files.walk(startWalk, depth)) {
            String walkedFile = stream1.map(String::valueOf).filter(path -> {
                return String.valueOf(path).endsWith("IntelGFX.log");
            })
                    .sorted().collect(Collectors.joining());
            System.out.println("walkedFile = " + walkedFile);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
**************
package algorithmes;

class Solution {

    static void printResult(Change m, long s) {
        // Change m = Solution2.optimalChange(s);

        System.out.println();
        if (m == null)
            System.out.println("given money " + s + " return null");
        else {
            System.out.println("Coin(s)  2€: " + m.coin2);
            System.out.println("Bill(s)  5€: " + m.bill5);
            System.out.println("Bill(s) 10€: " + m.bill10);
        }
    }

    // Do not modify this method​​​​​​​‌‌‌‌‌​​‌‌​‌‌‌‌​​‌​‌​​‌‌‌ signature
    static Change optimalChange(long s) {

        // Integral values
        long remaining = 0;
        long NbrOfBill10 = 0;
        long NbrOfBill5 = 0;
        long NbrOfCoin2 = 0;

        NbrOfBill10 = s / 10;
        remaining = s % 10;

        NbrOfBill5 = remaining / 5;
        remaining = remaining % 5;

        if (remaining < 2) {
            // (NbrOfBill5 * 5) + 1
        } else {
            NbrOfCoin2 = remaining / 2;
            remaining = remaining % 2;
        }

        System.out.println();
        System.out.println("amount to change = " + s);
        System.out.println("____________________________");
        System.out.println("NbrOfCoin2  2€: " + NbrOfCoin2);
        System.out.println("NbrOfBill5  5€: " + NbrOfBill5);
        System.out.println("NbrOfBill10 10€: " + NbrOfBill10);

        System.out.println("remaining : " + remaining);

        // return null if change cannot be rendered
        if (remaining != 0)
            return null;

        Change change = new Change();
        change.coin2 = NbrOfCoin2;
        change.bill5 = NbrOfBill5;
        change.bill10 = NbrOfBill10;
        return change;

    }

    static Change optimalChange2(long changeDue) {

        // Integral values
        long NbrOfBill10 = 0;
        long NbrOfBill5 = 0;
        long NbrOfCoin2 = 0;

        long remaining = changeDue;

        NbrOfBill10 = Math.round(remaining / 10);
        remaining = remaining % 10;

        NbrOfBill5 = Math.round(remaining / 5);
        remaining = remaining % 5;

        if (remaining < 2) {
            remaining = (NbrOfBill5 * 5) + 1;
            if (remaining % 2 == 0) {
                NbrOfBill5 = 0;
                NbrOfCoin2 = Math.round(remaining / 2);
            }
        } else {
            NbrOfCoin2 = Math.round(remaining / 2);
        }
        remaining = remaining % 2;

        System.out.println();
        System.out.println("changeDue = " + changeDue);
        System.out.println("____________________________");
        System.out.println("NbrOfCoin2  2€: " + NbrOfCoin2);
        System.out.println("NbrOfBill5  5€: " + NbrOfBill5);
        System.out.println("NbrOfBill10 10€: " + NbrOfBill10);

        System.out.println("remaining : " + remaining);

        // return null if change cannot be rendered
        if (remaining != 0)
            return null;

        Change change = new Change();
        change.coin2 = NbrOfCoin2;
        change.bill5 = NbrOfBill5;
        change.bill10 = NbrOfBill10;
        return change;
    }
}
***********
package algorithmes;

import java.util.Arrays;

/**
 * Java program to find all permutations of a given String using recursion and
 * loop. For example, given a String "XYZ", this program will print all 6
 * possible permutations of * input e.g. XYZ, XZY, YXZ, YZX, ZXY, XYX
 *
 *  un annagramme c’est juste un élément de l’ensemble de toutes les permutations possibles d’une chaine de caractères donnée.
 *
 *  Une permutation circulaire, c'est un décalage, dont l'élément "poussé hors du tableau" est réinséré de l'autre côté.
 */
public class StringAnagramNoOrder {

    public static void main(String args[]) {

        System.out.println(isAnagramSort("ABCD", "ADBC"));

    }

    static boolean isAnagramSort(String string1, String string2) {
        if (string1.length() != string2.length()) {
            return false;
        }
        char[] a1 = string1.toCharArray();
        char[] a2 = string2.toCharArray();
        Arrays.sort(a1);
        Arrays.sort(a2);
        return Arrays.equals(a1, a2);
    }

    // cherche les anagrammes de l’ensemble des caracteres situés à partir de la position first jusqu’à la position n
    private static void anagram1(String word, int first) {
        // Fixer la lettre à la position de départ,
        // Trouver toutes les permutations circulaires à partir de cette lettre jusq’à la dernière
        // Et pour chaque permutation, chercher les anagrammes à partir de la lettre suivante

        char T[] = word.toCharArray();

        if ((T.length - first) <= 1){
            System.out.println(T);
        }else {
            for (int i = 0; i < T.length-first ; i++) {
                anagramRound(T, first);
                anagram1(word, first+1);
            }
        }
    }
    // permet de faire une permutation circulaire, a partir de la position i du tableau.
    private static void anagramRound(char T[],int i){
        //  Sauvegarder le premier element
        char temp = T[i];
        // Decaler tous les elements d’un rang vers la gauche, a partir de la position i+1
        for(int j=i;j < T.length-1;j++){
            T[j] = T[j+1];

        }
        // Remettre le premier element à la dernière position
        T[T.length-1]= temp;
    }
}
************
package algorithmes;

/**
 * Java program to find all permutations of a given String using recursion and
 * loop. For example, given a String "XYZ", this program will print all 6
 * possible permutations of * input e.g. XYZ, XZY, YXZ, YZX, ZXY, XYX
 *
 *  un annagramme c’est juste un élément de l’ensemble de toutes les permutations possibles d’une chaine de caractères donnée.
 *
 *  Une permutation circulaire, c'est un décalage, dont l'élément "poussé hors du tableau" est réinséré de l'autre côté.
 */
public class StringPermutations {

    public static void main(String args[]) {
        String in = "ABC";
        int right = in.length() -1;
        permutation(in, 0, right);
    }

    private static String swap(String mot, int pos1, int pos2) {
        char[] chars = mot.toCharArray();
        char temp = chars[pos1];
        chars[pos1] = chars[pos2];
        chars[pos2] = temp;
        return String.valueOf(chars);
    }
    private static void permutation (String mot, int left, int right) {
        if(left == right) {
            System.out.println(mot);
        } else {
            for(int i = left; i <= right; i++) {
                String swapped = swap(mot, left, i);
                permutation(swapped, left+1, right);
            }
        }
    }
}
**************
package algorithmes;

public class SwapTwoIntegers {

    public static void main(String[] args) {
        int a = 10;
        int b = 20;

        // one way using arithmetic operator e.g. + or -
        // won't work if sum overflows
        System.out.println("One way to swap two numbers without temp variable");
        System.out.printf("Before swap 'a': %d, 'b': %d %n", a, b);
        a = a + b;
        b = a - b; // actually (a + b) - (b), so now b is equal to a
        a = a - b; // (a + b) -(a), now a is equal to b

        System.out.printf("After swapping, 'a': %d, 'b': %d %n", a, b);

        // another example
        a = Integer.MIN_VALUE;
        b = Integer.MAX_VALUE;
        System.out.printf("Before swap 'a': %d, 'b': %d %n", a, b);
        a = (a + b) - (b = a);
        System.out.printf("After swapping, 'a': %d, 'b': %d %n", a, b);

        // Another way to swap integers without using temp variable is
        // by using XOR bitwise operator
        // Known as XOR trick
        System.out.println("Swap two integers without third variable using XOR bitwise Operator");
        int x = 30;
        int y = 60;

        System.out.printf("Before swap 'x': %d, 'y': %d %n", x, y);
        x = x ^ y;
        y = x ^ y;
        x = x ^ y;

        System.out.printf("After swapping, 'x': %d, 'y': %d %n", x, y);

/**
 * Output One way to swap two numbers without temp variable
 * Before swap 'a': 10, 'b': 20
 * After swapping, 'a': 20, 'b': 10
 * Before swap 'a': -2147483648, 'b': 2147483647
 * After swapping, 'a': 2147483647, 'b': -2147483648
 * Swap two integers without third variable using XOR bitwise Operator
 * Before swap 'x': 30, 'y': 60
 * After swapping, 'x': 60, 'y': 30
 */
    }

}
*****************
package Combination;

import java.util.ArrayList;

public class Combination {

    /**
     * Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.
     * <p>
     * For example, if n = 4 and k = 2, a
     * <p>
     * solution is: [ [2,4], [3,4], [2,3], [1,2], [1,3], [1,4], ]
     */

    public static void main(String[] args) {
        System.out.println("n= 4, k = 2, output : " + combine(4, 2));
    }

    public static ArrayList<ArrayList<Integer>> combine(int n, int k) {

        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        ArrayList<Integer> item = new ArrayList<Integer>();

        if (n <= 0 || n < k) {
            return result;
        }

        dfs(n, k, 1, item, result); // because it need to begin from 1

        return result;
    }

    private static void dfs(int n, int k, int start, ArrayList<Integer> item, ArrayList<ArrayList<Integer>> res) {
        if (item.size() == k) {
            res.add(new ArrayList<Integer>(item));
            return;
        }

        for (int i = start; i <= n; i++) {
            item.add(i);
            dfs(n, k, i + 1, item, res);
            item.remove(item.size() - 1);
        }
    }
}
*****************
package Combination;

import java.util.ArrayList;
import java.util.Arrays;

public class CombinationSum {

    // @formatter:off
    /**
     * Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the
     * candidate numbers sums to T. The same repeated number may be chosen from C unlimited number of times.
     *
     * Note: All numbers (including target) will be positive integers. Elements in a combination (a1, a2, ... , ak) must
     * be in non-descending order. (ie, a1 <= a2 <= ... <= ak). The solution set must not contain duplicate
     * combinations.
     *
     * For example, given candidate set 2,3,6,7 and target 7, A solution set is: [7] , [2, 2, 3]
     *
     */
    // @formatter:on
    public static void main(String[] args) {
        int[] candidates = { 2, 3, 6, 7 };
        System.out.println("combinationSum({2,3,6,7}, 7) : " + combinationSum(candidates, 7));
    }

    /**
     * first impression of this problem should be depth-first search(DFS). To solve DFS problem, recursion is a normal
     * implementation. Note that the candidates array is not sorted, we need to sort it first.
     */
    public static ArrayList<ArrayList<Integer>> combinationSum(int[] candidates, int target) {
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();

        if (candidates == null || candidates.length == 0)
            return result;

        ArrayList<Integer> current = new ArrayList<Integer>();
        Arrays.sort(candidates);

        combinationSum(candidates, target, 0, current, result);

        return result;
    }

    public static void combinationSum(int[] candidates, int target, int j, ArrayList<Integer> curr,
                                      ArrayList<ArrayList<Integer>> result) {
        if (target == 0) {
            ArrayList<Integer> temp = new ArrayList<Integer>(curr);
            result.add(temp);
            return;
        }

        for (int i = j; i < candidates.length; i++) {
            if (target < candidates[i])
                return;

            curr.add(candidates[i]);
            combinationSum(candidates, target - candidates[i], i, curr, result);
            curr.remove(curr.size() - 1);
        }
    }

}
**********
package readers;

import java.io.*;
import java.util.HashMap;
import java.util.Map;
import java.util.regex.Pattern;

public class ReadFile {

    /**
     * Build a Map of Word
     */
    public static Map<String, Integer> buildWordMap(String fileName) {
        // Using diamond operator for clean code
        Map<String, Integer> wordMap = new HashMap<>();
        // Using try-with-resource statement for automatic resource management
        try (FileInputStream fis = new FileInputStream(fileName);
             DataInputStream dis = new DataInputStream(fis);
             BufferedReader br = new BufferedReader(new InputStreamReader(dis))) {
            // words are separated by whitespace
            Pattern pattern = Pattern.compile("\\s+");
            String line = null;
            while ((line = br.readLine()) != null) {
                // do this if case sensitivity is not required i.e. Java = java
                line = line.toLowerCase();
                String[] words = pattern.split(line);

                for (String word : words) {
                    // increment the number of time word occurs
                    if (wordMap.containsKey(word)) {
                        wordMap.put(word, (wordMap.get(word) + 1));
                    }
                    // add new word
                    else {
                        wordMap.put(word, 1);
                    }
                }

            }

        } catch (IOException ioex) {
            ioex.printStackTrace();
        }
        return wordMap;
    }

}
***********
package readers;

import java.util.Scanner;

public class ReadKeyword {

    public static void main(String[] args) {
        read();
    }

    public static String read() {
        Scanner sc = new Scanner(System.in);
        System.out.println("Veuillez saisir un mot :");
        String str = sc.nextLine();
        System.out.println("Vous avez saisi : " + str);
        return str;
    }
}

*********
