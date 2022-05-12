## DiceGame

```Java

import java.util.*;

public class Main {

    public Main() {

        Scanner scan = new Scanner(System.in);
        System.out.println("How many iterations?");
        int numSims = scan.nextInt();

        System.out.println("How many dice?");
        int numDice = scan.nextInt();

        scan.close();

        System.out.println("Number of simulations was " + numSims + " using " + numDice + " dice.");

        // Score frequencies
        HashMap<Integer, Integer> map = simulate(numSims, numDice);

        // output frequencies
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {

            System.out.println("Total " + entry.getKey() + " occurs " + ((double) entry.getValue() / numSims)
                    + " occurred " + entry.getValue() + " times.");

        }
    }

    private HashMap simulate(int numSims, int numDice) {

        HashMap<Integer, Integer> map = new HashMap<>();

        // simulations
        for (int i = 0; i < numSims; i++) {

            // score from each game
            int score = getScore(numDice);

            // frequencies of the score
            if (map.containsKey(score)) {

                map.put(score, map.get(score) + 1);

            } else {

                map.put(score, 1);

            }
        }

        return map;
    }

    // Simulate a round
    private int getScore(int numDice) {

        int[] dice;
        Random r = new Random();

        // score for the game
        int score = 0;

        // simulates each round
        while (numDice > 0) {

            // # of 3's
            int threeCount = 0;

            dice = new int[numDice];
            // init
            for (int i = 0; i < numDice; i++) {

                // number between 0 and 6
                int random = r.nextInt(6) + 1;

                // how many threes we come across
                if (random == 3) {

                    threeCount++;

                } else {

                    dice[i] = random;

                }
            }

            // if we came across 3 we do not add to score and remove # of 3's
            if (threeCount > 0) {

                numDice = numDice - threeCount;

            } else {

                numDice--;

                // sort so we can take smallest int from front of array
                Arrays.sort(dice);
                score += dice[0];

            }
        }

        return score;
    }

    public static void main(String[] args) throws Exception {
        new Main();
    }
}

```