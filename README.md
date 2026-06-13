import java.util.Scanner;

public class StoryAdventureGame {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Player tracking states
        boolean hasAncientKey = false;
        boolean hasTorch = false;
        int playerHp = 100;

        System.out.println("==================================================");
        System.out.println("       THE MYSTERY OF IRONWOOD CHASM              ");
        System.out.println("==================================================");
        System.out.println("You wake up at a misty crossroads inside a deep chasm.");
        System.out.println("You remember nothing except a rumor of hidden treasure.");

        // --- SCENE 1: THE CROSSROADS ---
        System.out.println("\n--- SCENE 1: THE CROSSROADS ---");
        System.out.println("To your left, a narrow path winds into a Sunken Forest.");
        System.out.println("To your right, a dark, carved stone staircase leads down into a Cave.");
        System.out.println("1. Explore the Sunken Forest");
        System.out.println("2. Descend into the dark Cave");
        
        int choice1 = getValidInput(scanner, 1, 2);

        if (choice1 == 1) {
            // --- BRANCH A: THE SUNKEN FOREST ---
            System.out.println("\n--- SCENE 2: THE SUNKEN FOREST ---");
            System.out.println("The canopy blocks the sky. Moss hangs like curtains.");
            System.out.println("You stumble upon an abandoned merchant wagon, half-buried in mud.");
            System.out.println("1. Search the ruined wagon thoroughly");
            System.out.println("2. Ignore the wagon and push deeper into the trees");
            
            int choiceForest = getValidInput(scanner, 1, 2);

            if (choiceForest == 1) {
                hasAncientKey = true;
                hasTorch = true;
                System.out.println("\n> Inside a lockbox, you find an ANCIENT KEY and a still-usable TORCH!");
            } else {
                System.out.println("\n> You walk past. You find nothing but cold wind rustling the leaves.");
            }

            System.out.println("\nThe forest path loops around and forces you back to the stone staircase.");
            System.out.println("With nowhere else to go, you begin your descent into the dark Cave.");
        } else {
            // --- BRANCH B: DIRECT TO CAVE ---
            System.out.println("\n--- SCENE 2: THE DARK CAVE ---");
            System.out.println("You head straight down the stairs. It is pitch black.");
            System.out.println("Without a light source, you trip over loose rubble and tumble down!");
            playerHp -= 30;
            System.out.println("> Ouch! You lost 30 HP. Current HP: " + playerHp);
        }

        // --- SCENE 3: THE UNDERGROUND GATE ---
        System.out.println("\n--- SCENE 3: THE UNDERGROUND GATE ---");
        System.out.println("You arrive in a massive subterranean chamber.");
        System.out.println("Before you stands a colossal iron door sealed with a strange lock.");
        
        if (hasTorch) {
            System.out.println("Your torch illuminates a small hidden tunnel passing under the gate.");
        } else {
            System.out.println("It is too dark to see any alternative routes around the door.");
        }

        System.out.println("1. Try to open the main Iron Door");
        System.out.println("2. Inspect the surroundings");
        if (hasTorch) {
            System.out.println("3. Crawl through the illuminated hidden tunnel");
        }

        int maxChoice3 = hasTorch ? 3 : 2;
        int choice3 = getValidInput(scanner, 1, maxChoice3);

        // --- GAME ENDINGS ---
        System.out.println("\n==================================================");
        System.out.println("                   THE ENDING                     ");
        System.out.println("==================================================");

        if (choice3 == 1) {
            if (hasAncientKey) {
                System.out.println("SUCCESS! The Ancient Key fits perfectly into the massive lock.");
                System.out.println("The iron door groans open, revealing a chamber overflowing with gold.");
                System.out.println("*** ENDING 1: THE WEALTHY ADVENTURER ***");
            } else {
                System.out.println("The door is firmly locked. You try to force it open with your shoulder.");
                System.out.println("A magical trap triggers! A bolt of lightning strikes your chest.");
                System.out.println("*** ENDING 2: CURSED BY THE GATE ***");
            }
        } 
        else if (choice3 == 2) {
            System.out.println("You spend hours searching the dark chamber walls but find nothing.");
            System.out.println("Your rations run low, and you are forced to retreat empty-handed.");
            System.out.println("*** ENDING 3: LOST AND FORGOTTEN ***");
        } 
        else if (choice3 == 3) {
            System.out.println("You squeeze through the tight tunnel. You emerge behind the door.");
            System.out.println("You find an altar holding a glowing, magical amulet of immense power.");
            System.out.println("*** ENDING 4: THE ARCANE CHOSEN ***");
        }

        System.out.println("\nThank you for playing!");
        scanner.close();
    }

    // Helper method to ensure the user inputs a valid choice
    private static int getValidInput(Scanner scanner, int min, int max) {
        int choice = -1;
        while (choice < min || choice > max) {
            System.out.print("\nEnter choice (" + min + "-" + max + "): ");
            if (scanner.hasNextInt()) {
                choice = scanner.nextInt();
                if (choice < min || choice > max) {
                    System.out.println("That choice doesn't exist. Try again.");
                }
            } else {
                System.out.println("Please enter a valid number.");
                scanner.next(); // Clear invalid input
            }
        }
        return choice;
    }
}
