import java.util.*;

public class ChallengeGame {
    private List<Challenge> challenges;
    private List<User> users;
    private Scanner scanner;

    public ChallengeGame() {
        this.challenges = new ArrayList<>();
        this.users = new ArrayList<>();
        this.scanner = new Scanner(System.in);
    }

    // Method to generate a random challenge
    public void generateChallenge() {
        Random random = new Random();
        int reward = random.nextInt(50) + 10; // Random reward between 10 and 59
        Challenge challenge = new Challenge("Sample challenge description", reward);
        challenges.add(challenge);
        System.out.println("New challenge generated: " + challenge.getDescription());
    }

    // Method to display challenges to the user
    public void displayChallenges() {
        System.out.println("Available challenges:");
        int index = 1;
        for (Challenge challenge : challenges) {
            System.out.println(index + ". " + challenge.getDescription());
            index++;
        }
        // Additional challenges
        System.out.println(index + ". Fibonacci Sequence");
        System.out.println((index + 1) + ". Palindrome Checker");
        System.out.println((index + 2) + ". Prime Number Generator");
    }

    // Method to handle challenge solving by the user
    public void solveChallenge(User user, int challengeIndex) {
        Challenge challenge = challenges.get(challengeIndex);
        if (!challenge.isSolved()) {
            user.earnMoney(challenge.getReward());
            challenge.setSolved(true);
            System.out.println("Congratulations! You earned $" + challenge.getReward() + " for solving the challenge.");
        } else {
            System.out.println("Challenge already solved.");
        }
    }

    // Method to display user's money
    public void displayMoney(User user) {
        System.out.println("Money: $" + user.getMoney());
    }

    // Method to start the game
    public void startGame() {
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();
        User user = new User(name);
        users.add(user);
        System.out.println("Welcome, " + user.getName() + "! Let's start the game.");

        while (true) {
            System.out.println("\n1. Generate new challenge");
            System.out.println("2. Solve challenge");
            System.out.println("3. Display available challenges");
            System.out.println("4. Display money");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            int option = scanner.nextInt();
            scanner.nextLine(); // Consume newline character

            switch (option) {
                case 1:
                    generateChallenge();
                    break;
                case 2:
                    displayChallenges();
                    System.out.print("Choose a challenge to solve: ");
                    int challengeIndex = scanner.nextInt() - 1;
                    scanner.nextLine(); // Consume newline character
                    if (challengeIndex >= 0 && challengeIndex < challenges.size()) {
                        solveChallenge(user, challengeIndex);
                    } else {
                        System.out.println("Invalid challenge index.");
                    }
                    break;
                case 3:
                    displayChallenges();
                    break;
                case 4:
                    displayMoney(user);
                    break;
                case 5:
                    System.out.println("Exiting game. Goodbye, " + user.getName() + "!");
                    return;
                default:
                    System.out.println("Invalid option. Please choose again.");
            }
        }
    }

    // Additional challenge: Fibonacci Sequence
    public void generateFibonacciChallenge() {
        // Generate a random number to determine the length of the Fibonacci sequence
        Random random = new Random();
        int length = random.nextInt(10) + 5; // Random length between 5 and 14
        StringBuilder description = new StringBuilder("Generate the Fibonacci sequence of length " + length + ".\n");
        List<Integer> fibonacciSequence = new ArrayList<>();
        fibonacciSequence.add(0);
        fibonacciSequence.add(1);
        for (int i = 2; i < length; i++) {
            int nextFibonacciNumber = fibonacciSequence.get(i - 1) + fibonacciSequence.get(i - 2);
            fibonacciSequence.add(nextFibonacciNumber);
        }
        description.append("Example: ").append(fibonacciSequence);
        Challenge challenge = new Challenge(description.toString(), 20);
        challenges.add(challenge);
        System.out.println("New challenge generated: " + challenge.getDescription());
    }

    // Additional challenge: Palindrome Checker
    public void generatePalindromeChallenge() {
        StringBuilder description = new StringBuilder("Write a program to check if a given string is a palindrome.\n");
        description.append("A palindrome is a word, phrase, number, or other sequence of characters that reads the same forward and backward.\n");
        description.append("Example: radar, level, madam");
        Challenge challenge = new Challenge(description.toString(), 25);
        challenges.add(challenge);
        System.out.println("New challenge generated: " + challenge.getDescription());
    }

    // Additional challenge: Prime Number Generator
    public void generatePrimeNumberChallenge() {
        // Generate a random number to determine the upper limit for prime numbers
        Random random = new Random();
        int limit = random.nextInt(50) + 10; // Random limit between 10 and 59
        StringBuilder description = new StringBuilder("Generate all prime numbers up to " + limit + ".\n");
        List<Integer> primes = new ArrayList<>();
        for (int i = 2; i <= limit; i++) {
            boolean isPrime = true;
            for (int j = 2; j <= Math.sqrt(i); j++) {
                if (i % j == 0) {
                    isPrime = false;
                    break;
                }
            }
            if (isPrime) {
                primes.add(i);
            }
        }
        description.append("Example: ").append(primes);
        Challenge challenge = new Challenge(description.toString(), 30);
        challenges.add(challenge);
        System.out.println("New challenge generated: " + challenge.getDescription());
    }

    public static void main(String[] args) {
        ChallengeGame game = new ChallengeGame();
        game.startGame();
    }
}
// i think it's better to call some api of some challenge solving website rather than just writing them down
